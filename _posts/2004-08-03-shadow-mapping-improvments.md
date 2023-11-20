---
title: 'Shadow mapping improvments'
date: '2004-08-03T21:28:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: shadow-mapping-improvments/
tags:
    - '3D Programming'
---

**I implemented Point Light shadows, soft shadows on spot lights.**  
<span class="texte2">Soft shadows on point lights are still in progress, the result is not great so far. </span>

**I also implemented the tone mapping to the back buffer of a different size than the deferred buffers, not a hard thing to do.**  
<span class="texte2">Doing all the deferred stuff using a 400*400 resolution for a final back buffer of 600*600 saves you a lot of rendering time (actually is almost twice faster) for a final result, not that bad. Maybe we can improve the final quality using few pixel shader instructions during the tone mapping.</span>

 **Screenshots time:**   
<span class="texte2">600\*600 rendering target, using a deferred/back buffer ratio of 1, 5 spots lights lighting the whole buffer each.</span>

<span class="texte2"></span>

 ![](/assets/fromcs/SoftShadows_4.jpg)

 ![](/assets/fromcs/SoftShadows_5.jpg)

 ![](/assets/fromcs/SoftShadows_6.jpg)

 ![](/assets/fromcs/SoftShadows_7.jpg)

 <span class="texte">I know, rendering time is quite awful, but:</span>

 · Spot light lighting is currently NOT optimized and doing a loooots of stuffs (const/linear/quad attenuation, penumbra, emissive, ambient, diffuse, specular computing, soft shadow, etc…).

 · Each spot light is lighting the whole screen: 600\*600 = 360 000 pixels (doing 5 times = 1 800 000 of lit pixels).

 · Geometry here, doesn’t matter (and texturing too), MRT render time is about 0.15VBL, putting 500 times more faces will push it to 0.4, no big deal.

 Shadow map rendering is about 0.15 VBL for five renders into a 512\*512 D24X8 texture, yummy!

**More about point light shadows:**

 <span class="texte2">Point light shadows are rendered using a R32F cube map (256\*256 pixels for a face). The rendering time is bad compared to a spot which uses a 512\*512 D24X8 shadow map (using nVidia’s UltraShadow). But I’ll be able later to compute efficiently shadow casters and receivers which will certainly cut off 1-3 faces render of the cube map. </span>

As usual the code is not fully optimized, but the design/architecture is. One may be afraid to the rendering time, but when you know few things like each light is lighting the whole screen (I don’t compute the bounding volume for an optimized lighting yet), after few majors optimization it should be better.