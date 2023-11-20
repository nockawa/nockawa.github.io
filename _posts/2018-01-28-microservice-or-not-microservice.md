---
title: 'Microservice or not microservice&#8230;'
date: '2018-01-28T11:44:21+02:00'
author: 'Loïc Baumann'
layout: post
permalink: microservice-or-not-microservice/
tags:
    - Microservice
---

It is always a good thing to benefit from the point of view of others, things are never either black or white and to find your way in this grey area that you’ll have to define is certainly not easy.  
I really enjoyed reading [this article](http://www.dwmkerr.com/the-death-of-microservice-madness-in-2018/) from [@dwmkerr](https://twitter.com/dwmkerr) because it highlight many good points, the article’s title was carefully chosen to generate some “hype”, it certainly delivered.

But I have to say that after this, I saw a wave of negative opinions (even if many people defended the concept by writing comments on Dave’s blog) toward Microservice and I thought it could be useful for me to share my experience on the matter.

The trigger for me to get back at blogging after so many years is this [twitter post](https://twitter.com/KatNovakovic/status/957427701555527682) from Katrina Novakovic, which basically summarized Dave key arguments:

- Complexity for developers, operators &amp; #devops
- Requires expertise
- Poorly defined boundaries of real world systems
- Complexities of state &amp; communication often ignored
- \#Versioning can be hard
- \#Monoliths in disguise
- Distributed Transactions

Looking this way, I think it’d be harder to find more extreme than this point of view. Summarized this way make Microservice scary for sure!

**Few facts**

- **Silver bullet don’t exist**, in the real world and also in the programming/architecture world. Microservices won’t be the solution to everything! Every time there’s a hyper on something, some people become “expert” at it and then try to push the concept to solve everything. It leads the less experienced people to believe than a given pattern is the **ultimate** one, a mere dream…Always ending the same way.
- **Doing complex stuffs is easy while achieving simplicity is very hard**. One of my all-time favorite quote comes from Leonardo da Vinci:  
    *“Simplicity is the ultimate sophistication”* It became one of my mantra in my daily work, because when programming/architecture is concerned, something easy is really hard to achieve and when you create something complex you have to realize something: you’ve made it wrong.  
    Of course, we are not perfect, we will always make mistakes we won’t have the time to correct, but just acknowledging this is very important to improve yourself for the next opportunity you will have. Otherwise you will go deeper in the complexity, even embracing it, because you will feel “superior” compared to others “mortal people” that won’t be able to catch what you’ve done.

- If you directly transitioned from a monolith architecture to a Microservice one : **you will suffer!** We have here almost two extremes, would you think it would be that easy to switch? Hell no!  
    Unfortunately a lot of people make this mistake, most of the time they don’t have the choice: they are young pro and certainly inherit from an old monolithic architecture and when they finally get the chance to start from a clean slate, they go toward the extreme opposite, not realizing what will be the consequences which will lead them to a very complex solution. For this reason…
- **Shifting to Microservice is hard**, Rome wasn’t built in a day, neither your experience on the matter, although reading things may be able to save you from making some mistakes.

**Things to realize**

A Microservice architecture requires a lot of tooling and best practices to operate it correctly, if you’re not experienced nor ready in all of them, you will suffer:

- A **Continuous Delivery Chain** (CDC) is required, if you don’t commit/build/test/push package in an automated and versioned fashion you will certainly fail.
- One of the key principle to respect in architecture is “**low coupling of components**“.  
    You know, the thing that didn’t exist in your monolithic architecture which made you wanna die many times due to the famous butterfly effect: you touch one little thing at a given place and **bam**, you have regressions on other parts you never thought they were related.  
    If you don’t have experience designing and writing a low coupled architecture and code, then you will certainly fail.
- I’m not a pattern freak, someone who live by the dogma at all cost, but my advice is: try to learn [**Domain Driven Design**](https://en.wikipedia.org/wiki/Domain-driven_design), if you don’t get it, it will be hard to switch to Microservice. The very small grained approach of Microservice will requires most of the same constraints, so it will certainly be a good starting point to familiarize yourself with DDD.
- Having a Continuous Delivery Chain is a start, but it won’t be enough, having an orchestrator to automatically deploy, components to monitor the health and load of each service instance is almost mandatory.  
    Otherwise the operating cost (and complexity) will be certainly unbearable. As Dave Kerr mentioned in his article, there is a correlation between Microservice and DevOps. I would say more precisely: you can’t do Microservice if you’re not already good at DevOps.

**My point of view, more detailed**

Here is what I have to say on each of the main points of Dave’s article:

- **Complexity for developers, operators &amp; #devops**: nothing is complex when you master them. I stated above, you have to be good at DevOps principles if you want to have a chance. You won’t build a Microservice architecture in one day.
- **Requires expertise**: well another open door to blast… Everything requires expertise, even a Monolithic architecture, it’s just that some things are easier to gain expertise at than others.
- **Poorly defined boundaries of real world systems**: this is not relevant to Microservice, look at DDD first…
- **Complexities of state &amp; communication often ignored**: this one deserve its own explanation below.
- **Versioning can be hard**: because versioning can be easy? More from this below.
- **Monoliths in disguise**: Your Microservice architecture certainly doesn’t sound like mine, but I believe that failing at designing low coupled services, lack of knowledge at DDD and Versioning issues lead you to an architecture of many services that end up be tied up ones to others, then forcing you an update of most of your architecture every time you make a minor upgrade. Microservice architecture didn’t fail you, you failed it.
- **Distributed Transactions**: more below…

**Complexities of state &amp; communication**

For me, most of your Microservice architecture has to be stateless, easier said than done I agree, but you have to employ at least two layers in your architecture:

1. The top level one, which answers the request from your client, whatever it’s a rich desktop, web or third-party service, here you will take care of things like: authentication, authorization, session state management (using Redis, NCache, Geode or whatever suits you) and security based cross-cuttings. This layer will be the visible surface of your architecture, you certainly don’t have to expose the whole architecture to the rest of the world (yes, your rich desktop, web client are part of “another world” for the sake of achieving low-coupling.)
2. The rest of your architecture will be stateless services where you can communicate freely, without fear of security issues and always carrying the minimal state (which will **always** be a subset of the actual client’s state) to perform the operation.

**Versioning can be hard**

Yes, it’s always is… That’s why we have ALM, DevOps and tones of disciplines I won’t mention (everyone will be his/her favorite) to deal with this. But whatever you’re doing you have to realize/accept few things:

- **Backward compatibility is a must**, it must be maintained at the Service’s Interface declaration at run-time level. If you’re from the .net world, [this post](https://stackoverflow.com/questions/1456785/a-definitive-guide-to-api-breaking-changes-in-net) will be helpful. If you fail to do so, yes, you will end up with a “monoliths in disguise”, but that’s the same of everything else: if you need to recompile the client when you make an upgrade at an interface it uses: you failed. You don’t need microservice to fail that, just two DLL talking are enough.
- So please respect the [**SemVer**](https://semver.org/) **principles** and don’t be afraid of doing a brand new interface as a new Major Version when you will break backward compatibility. It should not harm your Microservice architecture if you have a CDC and everything that monitors, handles scale up **and down** through automated deployment (and cleanup). If nobody uses your V1 of a given service anymore, it will end up in your architecture with a couple of instances, running for almost nothing, being decommissioned eventually by a human or a machine.
- Low-coupling, DDD, again, will be essential to success.

**Distributed Transactions**

I don’t see why distributed transaction are a requirement doing Microservices, I never used that and always find my way of doing things.

One of the key fundamental of Microservice is a very fine grained solution, a Service operation shouldn’t last forever executing, hence, when you really require transaction through many nested call, if you rely on synchronous call with each operation declaring its own transaction, then reporting as it should the success or failure of its execution, then the caller can commit or rollback its own transaction: no big deal.

If you start async everywhere, even when it’s not needed, ok, things are going to be tougher…

**Conclusion**

For me, server-side architecture and development is definitely challenging, you can do a very simple (and working at some extend) architecture that will be for on-premise solutions, but when you’ll go for SaaS you will definitely stumble upon things like: high availability, scaling, mutualized architecture, using PaaS solutions and it will be a whole different world.

Whatever the architecture you employ, if you don’t do it the right way, you will fail because the result will be overly complex. I agree that Microservice is a complex architecture so far, so jumping to this should be done with extreme caution. Is it a silver bullet? Nope, it won’t be the solution to everything, big companies rely on it because they have the skills, they can afford it and above all: they need it.

That being said I don’t rule out this architecture for smaller companies, it will be certainly harder for them, but there are more and more solutions that will assist you ([read this](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-overview-microservices) for instance).

I always welcome all the point of views because, even if the tone of this post doesn’t suggest it *at all*, I will always be open minded and learn from others. The hype around new techs in our industry is something that bring us as many good things as bad ones. One day a given tech is the solution to everything, the day after it will be crucified by everyone, for the sake of a new tech, most of the time.

Microservice are being crucified and we’re entering the era of serverless architecture: the true, first, and only one silver bullet that will ease all our pain!

Does it look like something we’ve already saw before? Hum… 🙂