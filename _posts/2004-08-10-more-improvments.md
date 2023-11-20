---
title: 'More improvments&#8230;'
date: '2004-08-10T21:26:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: more-improvments/
tags:
    - '3D Programming'
---

 **Added projector texture for Point and Spot lights.**   
<span class="texte2">A cube map is used for the Point Light and a 2D texture for the spot, both are almost free concerning the rendering time.</span>

 **Parallax mapping is almost done.**   
<span class="texte2">The technique itself is quite simple, but it implies many little things to get it “practical” and be able to produce graphic content using it.</span>

 **Every effects/techniques implemented so far are “practical”.** <span class="texte2">That means you can produce 3D with them for a games of other kind of real-time applications, it’s not just for demo/screenshot! 🙂</span>

 **Improved the compatibility of the renderer with the logical 3D engine.**

 **I’ve made some tests of Sub-surface scattering.** <span class="texte2">   
(the light ray going through a given object and lighting it on the other side).</span>

 **And at last I did a bit of performance tuning/optimisation, rearranged the main fx file which is starting to be big! 🙂**

 **Ok some random screenshots, not sphere/cube/coder art this time…**

 ![](/assets/fromcs/Indoor_1.jpg)

 ![](/assets/fromcs/Indoor_2.jpg)

 ![](/assets/fromcs/Indoor_3.jpg)  
<span>If you look closely, the shadows are not accurate at some places, this was a minor bug that was fixed, but I was too lazy to start the screenshots again.maybe later!</span>

 <span>![](/assets/fromcs/Poly48K_4Points.jpg)  
<span>50K faces, 4 point lights</span></span>

 <span><span>![](/assets/fromcs/Poly48K_4Spots.jpg)  
<span>50K faces, 4 spotlights</span></span></span>

 <span><span><span>![](/assets/fromcs/Poly400K_1Direct.jpg)  
<span>400K faces, 1 direct light</span></span></span></span>

 <span><span><span><span>![](/assets/fromcs/Poly400K_1Direct_1Point.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">400K faces, 1 direct and 1 point light</span></span></span></span></span>

**More about the renderer architecture:**

The 3D Engine is totally logical, it doesn’t have any dependencies with a given platform or hardware.  
There is an abstract renderer interface which can be used to develop new renderers (XBox, OpenGL, DX7, DX8, DX9SM3 were tested/implemented so far).  
If one wish to build is own renderer from scratch, no big deal, you don’t have to use this abstract interface if you don’t want to. The main reason is the rendering pipeline is not straight forward processed, but somewhat reversed processed: the 3D Engine won’t feed the renderer with 3D data (meshes, lights, etc.) but the renderer will take the data itself. Optimal computation/update of the data is provided: is computed only what the renderer needs, etc.

**More about sub-surface scattering:**

The technique can be easily implemented in the renderer and the production pipeline (one global density factor, and a texture for per-texel info), but I’m afraid that it doesn’t worth it. The main issue is I have to read the light Z-Buffer, and I can’t do it for direct and spot lights when using the nVidia’s UltraShadow. The concrete application of such effect is rare I guess, that’s why I’m putting it aside for now.