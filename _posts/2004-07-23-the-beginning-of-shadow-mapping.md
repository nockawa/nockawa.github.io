---
title: 'The beginning of shadow mapping'
date: '2004-07-23T21:29:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: the-beginning-of-shadow-mapping
tags:
    - '3D Programming'
---

 **Implemented the spot light rendering.**   
<span class="texte2">I have now the three basic types of light: directional, point and spot</span>

 **Added a Gaussian filter after the creation of the Occlusion Map.**   
<span class="texte2">The results speak themselves, that is definitely a must have!</span>

 **The nightmare has begun: shadows…** <span class="texte2">I knew that would be one of the hardest parts of the rendering (if not the hardest), and it is…   
As usual, I started by reading many papers and slideshows.I also looked the archives of the GD-Algorithms mailing list, and put back the topic because people there were apparently silent since one year ago. </span>

Between the two families, as I rely on the pixel power, my choice naturally tends to Shadow Maps. In the land of shadow maps, many people have different opinions about what is the best to use, and with time passing, it doesn’t seem to converge into one particular technique.   
Single buffer, multiple buffers, post perspective or not, trapezoidal, done in light space, oh my god…

Before starting to ask for people’s opinion, I had faith into the Perspective Shadow Mapping (aka PSM), after reading its revision from Simon Kozlov in the GPU Gems. Many people still say it’s not a viable technique, because of its numerous special cases which are really hard to solve.

The only thing everybody agrees is to make the most effort to limit the viewing frustum of the light, so I guess I’m starting from this point, and will head later on the PSM.   
For now, I’ve implemented the basic of shadow mapping. Precision and point lights are coming next…

Trying to gain more precision, I first tried to make the depth comparison using a R32F buffer instead of the Depth Buffer. So I had to render my scene in that buffer, which is 60% slower than into the Depth Buffer only (from my tests).   
The whole thing doesn’t worth it, it’s slower, and as it’s not using the Z-Bias, the result is pretty bad (and I really don’t want to make a Pixel Shader to emulate it). So I stick with fast rendering D24X8 surface.

 **I would like to thank Mark Harris from nVidia for his advices and support.**

 **Screenshots:**

 ![](/assets/fromcs/Shadows_1.jpg)

![](/assets/fromcs/Shadows_3.jpg)  
Basic shadow mapping