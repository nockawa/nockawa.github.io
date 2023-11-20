---
title: 'Two months later&#8230;'
date: '2004-10-19T21:24:00+02:00'
author: 'Loïc Baumann'
layout: post
permalink: two-months-later/
tags:
    - '3D Programming'
---

 <span class="texte2">I was working on something else (and took holidays), didn’t have the time to go back to the renderer until three weeks ago.   
At first I wasn’t considering these three weeks work as a part of the SM3 Renderer, so I didn’t want to update this page.</span>

 But well, even if it’s not talking about a cool rendering technique, it’s still part of this project, and this is something I’d like to share too.

 **Here we go, let’s catching up with my new in-viewport GUI.**

 **Windowing System and redraw.**   
<span class="texte2">There were three criteria to pay attention to: fast display of windows, make good use of the Alpha, having the whole system as flexible as possible.</span>

 The GUI is system is like the others, you have windows organized in a hierarchical way. There’re notions of active windows, focus window, “hover” window. You can capture mouse events (and stack the captures). There’s a global alpha constant for the GUI and for each top level windows, which is used by all the low level drawing methods (DrawRect, FillRect, DrawLineList, DrawMesh, DrawTexture, etc…) for fading effects. Redraw had to be optimal so I’m also using clipping region (using D3D Scissor Rect).

 Rendering the windows’ content was obviously a big concern and not an easy task when you want things to be fast, flexible and with transparency. The most important feature of this system is you can decide for EACH windows (even child ones) if you want it to be cached in a texture. This way, if the window’s content doesn’t change, the cached texture will be used instead of redrawing everything. When a window is cached in a texture, it will also render into this cache the content of its child windows as long as the given child is not a also cached window. You can think about the benefits of having a hierarchical caching system.

 Optimal redraw requests are made for transparent windows, using optimal computing of the transparent regions across the hierarchy.

 <span class="texte2"></span>**Draw text, font and stuffs.**   
<span class="texte2">I had to extend the font system Ihad (which was fairly simple). More font styles are supported, there’s a font pool now used to avoid redundant creation of identical font pages. I also recorded properties such as font ascenders, descenders, spacing, etc. Added methods to compute the size taken by a given letter, word, line or text (bound by a logical area).</span>

 Drawing text is now more complete, you can specify a bounding zone, an alignemnt, auto wrapping, and auto display of an ellipsis if the line is truncated..

 **HTML Document display.**   
<span class="texte2">Ok, I have to admit, it was not a necessary thing, but well, I thought it would be a good test for the GUI (and also a challenge for me). At first I only wanted to do a multi-line edit control, but after I wanted to display more complex text formatting (color, underline, bold, font change), so I looked the Rich Text format. And when I realized it was more messy than the HTML one, I choosed the HTML (also because it’s way more popular now).   
I won’t explained in detail the structure, but I’m kind of proud of it. It’s very efficient and flexible (and I’ll be able later to upgrade it to edit HTML content). I of course don’t support all the HTML tokens (far from it), but the structure is open and it’s easy to add the support of new ones.</span>

 <span class="texte">**Other controls**   
</span><span class="texte2">So I have now the following high level classes: </span>

<span class="texte2"></span><span class="texte2"></span>

- BaseWnd: the abstract class that all other windows are derived from.
- Window: a top level window.
- Control: abstract class for control typed windows.
- Menu: to display a menu.
- ObjIcon: display an icon of a given object, the icon is a 3D render of a mesh lighted with a global light. The mesh is chose from the type of the object which is viewed.
- ObjExplorer: a little object browser to walk through a given object database (a 3D scene, the SM3 rendering architecture, IML Framework for instances)
- EditCtrl: single/multi line display, HTML display, encoding from raw or C style text, raw text editing (stored in HTML).   
    <span class="texte2">The ObjExplorer class is still not finished, I’m currently working on the generic Drag n’ Drop system (which will be heavily used). </span>
    
    <span class="texte2">**Screenshots:**</span>
    
     ![](/assets/fromcs/GUI_1.jpg)  
    This is how it looks like when I start my Test3DE.exe now.
    
    ![](/assets/fromcs/GUI_2.jpg)  
    The Object explorer with a nice tool-tip that displays the content of a DirectX Texture.
    
    ![](/assets/fromcs/GUI_3.jpg)  
    The object explorer displays the content of a Resource Pack (the main one of the scene)
    
    ![](/assets/fromcs/GUI_4.jpg)  
    The tool-tip displays the content of a DirectX texture which is… the IML Console’s one.
    
    ![](/assets/fromcs/GUI_5.jpg)  
    Just to show what a menu looks like