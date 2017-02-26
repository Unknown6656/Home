---
layout: post
type: blog
title:  "Welcome to Six Labors!"
date:   2017-02-26 12:52:00
categories: update shapes fonts
author: tocsoft
snippet: A start of things to come.
---

Welcome to Six Labors. Six Labors is a group of related open source projects huddling together for safty.

As of today we have 2 main projects.

## [Shapes](http://github.com/sixlabors/Shapes)

Shapes is a 2D polygon manipulation and interogation library written in c# and targets .netstandard 1.1 making it entirely crossplatform and will run on everything from android phone, to windows desktops, to linxus servers and everything in between. 

Shapes is currently still in alpha but is being used by [ImageShape][imagesharp]  for is line and vector drawing code.


## [Fonts](http://github.com/sixlabors/Fonts)

Fonts is an true type/woff compatible font loading library written in c# and targets .netstandard 1.1 making it entirely crossplatform and will run on everything from android phone, to windows desktops, to linxus servers and everything in between. 

Fonts provides text measuring, layout, and abstracted rendering systems. You just need to plugin your own raserizer (like ImageSharp)

Fonts is currently still in alpha but is about to be used by [ImageShape][imagesharp] for is text drawing code. (this is still in progress)


[imagesharp]: https://github.com/jimBobSquarePants/ImageSharp "ImageSharp"