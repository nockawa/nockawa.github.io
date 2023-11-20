---
title: 'First shot of the renderer'
date: '2004-07-17T21:31:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: first-shot-of-the-renderer/
tags:
    - '3D Programming'
---

**I’ve spent too much time the last few days to make D3DX working with Irion.**  
<span class="texte2">The library is static, and doesn’t like our custom new/delete operators. The bug is not solved yet (appears to be a problem on the Microsoft’s side), but I temporary bypassed it. </span>

**Big big thank to Greeg Peeper from Microsoft for his help and support!**

 **HLSL and D3D .FX roxx**   
<span class="texte2">It eases and speeds the work so much. I had several problems (still the mysterious D3DX bug) to compile/open a .fx file in my project, but I guess it only happens to me…</span>

 <span class="texte2"></span>**So I started a new Renderer project (IrionSM3Renderer)**   
<span class="texte2">Ripped a lot of the code from the IrionDX9Renderer one (Vertex Buffer and other D3D resources creation and maintenance).</span>

 <span class="texte2"></span>**Let’s go for the Deferred Shading.**

<span class="texte2">**1) Created three Rendering Targets, 32bits wide each.**   
The first is D3DFMT\_A8R8G8B8 to store the albedo.   
The second is D3DFMT\_R32F to store the pixel’s Z.   
The third is D3DFMT\_G16R16F to store the X and Y components of the pixel’s normal.   
I think I’ll need a fourth one later to add material properties. </span>

**2) Program the following rendering passes:**   
• Rendering into the MRTs. Nothing complex, except a little detail I explain below.   
• Do the lighting, for each light I parse the MRTs, computing the lighting for each pixel and accumulate the result in a D3DFMT\_A16B16G16R16F buffer (why bother).   
• Display the accumulation buffer by copying it in the back buffer (have to take care of few things to make the 3D GUI Helpers still rendering with the standard path).

As usual, I had few matrices issues, and I also didn’t realised that storing data in the Rendering Target can only be in the \[0, 1\] range and not \[-1, 1\] (like the normals…).

All the data are transformed into the camera’s space, I can reconstruct the Normal ’s Z (Z = sqrt(1-X²-Y²)) as I don’t mind about the sign of the vector (always positive in camera’s space).

 <span class="texte2"></span>**That’s all for now…Diffuse and Specular lighting is done, with a basic material.**

 **I modified the Test3D program**   
<span class="texte2">to be able to switch on the fly between the DX9Renderer and the SM3Renderer.   
It’s great, I can see the differences instantaneously!</span>

 <span class="texte2">**Screenshots Time!**</span>

 <span class="texte2">![](/assets/fromcs/Render1_SM3.jpg)</span>

 <span class="texte2"><span class="texte">Per pixel lighting, yummy.</span></span>

 <span class="texte2"><span class="texte"><span class="texte">Note: the lighting is not the exact same one because I don’t take into account all the material settings. The specular is not at the same place as the FFP version, I think I’ll figure it out later. </span></span></span>

 <span class="texte2"><span class="texte"><span class="texte">![](/assets/fromcs/Render1_DX9.jpg)</span></span></span>

DX9 Fixed Function Pipeline version.