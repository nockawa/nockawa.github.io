---
title: 'New rendering features !'
date: '2004-08-24T21:25:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: new-rendering-features/
tags:
    - '3D Programming'
---

 **I added Gamma Correction, bump/normal mapping, and Depth of Field.**

 **I also fixed few bugs.**

 **ScreenShots of Gamma Correction**

 It’s brighter where it should be, and still dark where it should be too.

<span class="texte">The picture was took from the ATI’s sRGB sample.</span><span lang="EN-GB" style="mso-ansi-language: en-gb"></span>

 ![](/assets/fromcs/PicNoGammaCorrected.jpg)  
No correction

 ![](/assets/fromcs/PicGammaCorrected.jpg)  
Gamma corrected

 **ScreenShots of Normal Mapping**

 ![](/assets/fromcs/NormalMap_Solid.jpg)  
The left sphere is the high poly one (40K faces). The right is the low poly version (960 faces) with the normal map applied.   
The normal map was created with our 3D Studio Max <span class="lien1">Bump-o-matic</span> plugin.

 ![](/assets/fromcs/NormalMap_Wire.jpg)  
Wire version of the first screenshot.

 ![](/assets/fromcs/NormalMap_Normals.jpg)  
Rendering of the normals.

 **ScreenShots of Depth of Field**

 ![](/assets/fromcs/DepthOfField_1.jpg)  
The white AABBs symbolize the Plane in Focus. Check their intersection with the scene to get a better idea of their position.

 ![](/assets/fromcs/DepthOfField_2.jpg)

 ![](/assets/fromcs/DepthOfField_3.jpg)

**More about depth-of-field:**

I read many things about Depth of Field, the article in GPU Gems for instance, saw many formula without really knowing how to practically implement them.

So I came out with an in-house one, really simple:  
 **Df** = **DP** \* abs(**PosZ** – **PiF**) / **PosZ**.  
 **DP** is the Depth of Field Power. 0 to disable it, 1 for standard result, &gt;1 to get something really blurry.  
 **PosZ** is the position in camera space of the pixel to compute.  
 **PiF** is the Plane in Focus position in camera space.  
 **Df** is the result, I clamp it to \[0,1\] and use it in the lerp from the accumulation buffer and the blurred one during the ToneMapping.