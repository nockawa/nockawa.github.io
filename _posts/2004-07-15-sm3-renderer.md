---
title: 'SM3 Renderer'
date: '2004-07-15T21:32:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: sm3-renderer/
tags:
    - '3D Programming'
---

Ok, I have my new GeForce 6800 GT, the latest beta of the DirectX 9.0c SDK, the latest beta of nVidia’s drivers (SM3 enabled). Let’s start!

I read many papers, watched some samples, I’m getting back in the 3D programming slowly as I spent the past month working on 3D Editor and game logic.

Few words come to my mind: <span class="texte2">Perspective Shadow Mapping, Parallax Mapping, Ambient Occlusion, HDR, and Deferred Shading.</span>

The most critical part of the brainstorming was: should I go for the Deferred Shading?

I mean the whole technique is really appealing:  
<span class="texte2">• It’s suited for hardware like the R300 and NV40 (good precision, Multiple Rendering Targets).   
• Come on, true per-pixel lighting!   
• Distinct stages for the rending process: albedo computation/MRT setup, lighting, post process (HDR, Blur, Fog, Glow …), which means high plugability!   
• Perspective Shadow Mapping should work nicely with.   
• It should only get better and faster on next hardware.   
</span>  
But:  
<span class="texte2">• Hum…transparency? How? Where?   
• Antialising…not so much, but we can walk round this.   
• Can’t use complex Materials such as the ones for SH lighting.   
• High pixel power is needed, can this technique run a great game scene at a suitable framerate on a X800 or 6800 GT?   
</span>  
Ok, let’s do it, the technique itself is so attractive to me, I have to try it out!