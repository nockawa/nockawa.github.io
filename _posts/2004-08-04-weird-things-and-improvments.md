---
title: 'Weird things and improvments'
date: '2004-08-04T21:27:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: weird-things-and-improvments/
tags:
    - '3D Programming'
---

 **Ok for some mysterious reasons using four MRTs can generate big slow down on the 6800.**   
<span class="texte2">So I separated the render of the MRT in two passes, the first one renders the Z-Buffer and the Z-MRT, the second one renders the three other MRTs (albedo, normal, material settings).   
This way the second pass took advantage of the Z Culling, sometime pixel shaders can be heavy when funky stuffs are done to compute the albedo, this should be faster when it’s the case.   
On the performance side, it’s always faster, regardless the vertices count of the meshes.</span>

 **I’ve finalized the soft shadows on point lights.**   
<span class="texte2">I’m using only two samples, the vector used to address the cube map is slightly disrupted from the position of the pixel being rendered. I can’t say it’s perfect or nice, but well, it’s fast. Four samples instead of one make the whole lighting pass 50% slower!</span>

 **I also fixed few bugs.**

 **Screenshots:**

 ![](/assets/fromcs/PointSoftShadows_1.jpg)

![](/assets/fromcs/PointSoftShadows_2.jpg)

![](/assets/fromcs/PointSoftShadows_3.jpg)

![](/assets/fromcs/PointSoftShadows_4.jpg)  
A 256\*256 Cube map is used. The render time of the shadow map is not bad, about 10% of the VBL.