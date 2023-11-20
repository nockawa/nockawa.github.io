---
title: 'Parallax mapping, more ambient occlusion n&#8217; stuffs'
date: '2004-08-16T21:26:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: parallax-mapping-more-ambient-occlusion-n-stuffs/
tags:
    - '3D Programming'
---

 **Parallax mapping is finished.**   
<span class="texte2">The whole production pipeline is now ready for that technique. The 3D Studio MAX plugin now computes the correct scale/bias and can also display the result in a custom view.</span>

 **Screenshots**

 ![](/assets/fromcs/sc_para_nobump.jpg)

 ![](/assets/fromcs/sc_para_with.jpg)  
As you can see, the specular highlight is not ‘real’ for that kind of material (supposed to be rocks…)

 ![](/assets/fromcs/sc_para_wire.jpg)  
Wireframe mode!

 **I added a new parameter in the Ambient Occlusion Map creation**    
<span class="texte2">which is the length of the rays used to perform the occlusion test. This way the occlusion map builder can now produce maps for indoor meshes.</span>

 **Screenshots**

 ![](/assets/fromcs/sc_ambocc_off.jpg)   
Ambient occlusion off

 ![](/assets/fromcs/sc_ambocc_on.jpg)  
Ambient occlusion on

 ![](/assets/fromcs/sc_ambocc2_off.jpg)  
Ambient occluion off

 ![](/assets/fromcs/sc_ambocc2_on.jpg)  
Ambient occlusion on

 ![](/assets/fromcs/GrRoomAOM.jpg)  
Ambient occlusion map

 ![](/assets/fromcs/sc_ambocc_max_uvw.jpg)  
3DS Max UVW unwrap modifier

 ![](/assets/fromcs/sc_ambocc_bumpo.jpg)  
The original mesh of the room wasn’t mapped, so I used the flatten mapping of the UVW Unwrap modifier of 3DS MAX to generate mapping coordinates, then use the Bum-o-matic plugin to generate the Ambient Occlusion Map.

The result speaks itself.

 **Light volume rendering.** <span class="texte2">Before, for each light was lighting every pixel on the viewport, which was quite slow/wasteful. Now for point and spot lights, their bounding volume is rendered to perform the lighting, as you can guess, this is much faster for small area lights.</span>

 <span class="texte2"></span>**Screenshots**

 ![](/assets/fromcs/Indoor_17.jpg)  
Without

 ![](/assets/fromcs/Indoor_17V.jpg)  
With

 ![](/assets/fromcs/sc_lightvol_off.jpg)  
Without

 ![](/assets/fromcs/sc_lightvol_on.jpg)  
With

 **I Added an IML Console right in the viewport.** <span class="texte2">Having more and more rendering parameters I’d like to tweak in real-time, I’ve decided to take advantage of the whole IML architecture to interact with the renderer (and the 3D Scene) in run-time.</span>

 **Screenshots**

 ![](/assets/fromcs/sc_IMLConsole.jpg)

 **More about Ambient Occlusion builder:**

For each pixel on the map we’re created, its position into the mesh is located, and a series of rays are thrown to perform occlusion tests (intersection) with other part of the mesh itself. The problem for indoor environments is there’s always a intersection found (because the mesh is closed), making it impossible to produce an accurate map. By letting the graphist set a length for the rays that are cast, the occlusion can be perform on a limited area, then producing the expected result.

**More about IML:**

IML stands for *Irion Micro Language*, it’s a run-time wrapper to the C++ components, for each Irion component one is developing, he can create an IML Class that will be used to expose the component to the IML Framework. Using IML via an IML Console, you can create/edit/delete new components or existing ones. For instance, I developed an IML Class to wrap the SM3Viewport C++ class, I exposed a set of properties (rendering modes, rendering attributes, stats display, etc.) that can be later modified via an IML Console or Script.