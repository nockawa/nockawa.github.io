---
title: 'Updating the lighting'
date: '2004-07-19T21:30:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: updating-the-lighting/
tags:
    - '3D Programming'
---

**Not much, I made the renderer plug-able for our shaders, add a better lighting support (see screenshots).**

 **I added a fourth Render Target.**   
<span class="texte2">The surface type is D3DFMT\_A8R8G8B8, it stores the specular intensity, specular power, and occlusion factor (not computed actually).</span>

**I also tried to palletize the Material settings.** <span class="texte2">I made the whole dynamic system which stores all the materials’ settings into a texture, with a look up index stored per pixel in the MRT. Everything went fine and smooth, but I dropped it because I don’t have the feeling it’s something necessary.</span>

 <span class="texte2"></span>**Read many papers on subsurface scattering, ambient occlusion and parallax mapping.** <span class="texte2">I had to make sure everything could fit in the current architecture!</span>

 <span class="texte2">**Screenshots:**</span>

 <span class="texte2">**![](/assets/fromcs/Render_PointNDirect_SM3.jpg)** <span class="texte">Deferred Shading renderer version! I like this!!! 🙂   
</span>The point light is red, has short range and a high power, the specular highlight looks great. And it’s hundred times better when you can move the camera and lights in real-time! 🙂 </span>

 <span class="texte2">![](/assets/fromcs/Render_PointNDirect_DX9.jpg)</span>

Standard Renderer version.  
The floor is a dumb square, so forget about specular lighting. The Point light (at the left) has a small range, that’s it does absolutely nothing on the floor.

**Screenshots of the intermediate buffers:**

![](/assets/fromcs/Buffer_Final.jpg)  
Final Render

![](/assets/fromcs/Buffer_Finall_NoToneMap.jpg)  
Final without Tonemap

![](/assets/fromcs/Buffer_Albedo.jpg)  
Albedo

![](/assets/fromcs/Buffer_Position.jpg)  
Position of each pixel in 3D space. Yes you can see the cylinder and the sphere, just look closer! 🙂

![](/assets/fromcs/Buffer_Depth.jpg)  
Depth of each pixel

![](/assets/fromcs/Buffer_Normal.jpg)  
Normal of each pixel

![](/assets/fromcs/Buffer_Blurred.jpg)  
Blurred version, used by the ToneMapping process