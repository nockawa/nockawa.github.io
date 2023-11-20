---
title: 'Ambient occlusion: done!'
date: '2004-07-20T21:30:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: ambient-occlusion-done/
tags:
    - '3D Programming'
---

<span class="texte2">I’ve programmed the routine to compute a texture storing the ambient occlusion of a given mesh. The result is as expected: great! (see the screenshots). </span>

The computing process can take a while, had to throw a lot of rays per texel to get an accurate result. 512 is a good number. So for a 256\*256 texture, you have at least 33 million rays thrown. When I say at least, it’s because if a given texel is shared by two faces of the mesh (across the edge), the double are thrown.

Thanks to the [opcode](http://www.codercorner.com/Opcode.htm) library, it doesn’t take forever…   
I’ll certainly add an option to filter the produced picture (useful when the ray count is low).

 **Screenshots:**

 The mesh (courtesy of [<span class="lien1" style="font-weight: normal">Bruno Dosso</span>](http://dionex.free.fr/)) is 12592 triangles and 6424 vertices.

 <span lang="EN-GB" style="mso-ansi-language: en-gb">Computed on a Athlon XP 2800+. You can see the render time in the texture’s window caption.</span>

 <span lang="EN-GB" style="mso-ansi-language: en-gb">![](/assets/fromcs/AmbOcc_256_256_L16_1024_Render_NoTex_Without.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">Basic rendering, no diffuse texture, no ambient occlusion texture.</span></span>

 <span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb">![](/assets/fromcs/AmbOcc_256_256_L16_1024_Render_Without.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">Diffuse Texture, without Ambient Occlusion</span></span></span>

²

 <span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb">![](/assets/fromcs/AmbOcc_256_256_L16_1024_Render_NoTex_With.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">256\*256 occlusion map, 16bits, 1024 rays per texel.</span></span></span></span>

 <span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb">![](/assets/fromcs/AmbOcc_256_256_L16_1024_Render_With.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">Same as left, with a diffuse texture.</span></span></span></span></span>

 <span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb"><span lang="EN-GB" style="mso-ansi-language: en-gb">![](/assets/fromcs/AmbOcc_256_256_L16_1024_Map.jpg)  
<span lang="EN-GB" style="mso-ansi-language: en-gb">The computed Ambient Occlusion Texture, done in 2min27sec.</span></span></span></span></span></span>