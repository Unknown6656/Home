---
layout: post
type: blog
title:  "Drawing a textual watermark on images using ImageSharp and SixLabors.Fonts"
date:   2017-04-08 09:53:00
tags: [fonts, ImageSharp, tips]
author: tocsoft
snippet: "Tips on using SixLabors.Fonts and ImageSharp"
---

Lets say you host an stock image marketplace where photographers can upload images and sell them, they are going to want to show previews of the images but with a large watermark overlaid to prevent people using the images without authorization. So how do we do that.

For this example we will be using [ImageSharp](http://imagesharp.net) for doing the heavy pixel lifting, which in turn uses [SixLabors.Fonts](http://fonts.sixlabors.com) for its text rendering and font loading engine.

So lets start off with the simplest version and build it up into a robust solution.

```c#
using(Image img = Image.Load("sourceImage.jpg"))
{
    // firstly you are going to need a font family, Lets just grab one from the system font store.
    FontFamily family = FontCollection.SystemFonts.Find("Arial");
    // now we need to get a particularly styled/sized version 
    Font font = new Font(family, 100f, FontStyle.Regular);
    // grey with 50% opacity
    Color fill = new Color(128, 128, 128, 128);
    // draws "Copyright Person Name" using Arial at 10pt at the top left of the image.
    img.DrawText("Copyright Person Name", font, fill, new Vector2(0,0))
}

```
Now we have drawn the text over the image lets look what that looks like 

[![Large Image with text overlay]({{ site.url }}/assets/posts/2017-04-08-watermarks/resized_large_simple.jpg)]({{ site.url }}/assets/posts/2017-04-08-watermarks/large_simple.jpg)

no too bad, could be position better but that shouldn't be too hard to fix. The real problems start showing up when we repeat it on a smaller image.

[![Small Image with cropped text overlay]({{ site.url }}/assets/posts/2017-04-08-watermarks/resized_small_simple.jpg)]({{ site.url }}/assets/posts/2017-04-08-watermarks/small_simple.jpg)

Well that's not what we want we want the text to scale based on the size of the image so lets do it.

[SixLabors.Fonts](http://fonts.sixlabors.com) has the useful `TextMeasurer` class that going to be perfect for us to use so we can calculate the perfect font size to use.

So how do we use it.

```c#
// firstly you are going to need a font family, Lets just grab one from the system font store.
FontFamily family = FontCollection.SystemFonts.Find("Arial");
// now we need to get a particularly styled/sized version 
Font font = new Font(family, 100f, FontStyle.Regular);
TextMeasurer measurer = new TextMeasurer();
// we can now get the dimensions of the bounding box of a piece of text
Size size = measurer.MeasureText("Copyright Person Name", font, 72); 
```
> NOTE: ImageSharp uses a standard DPI of 72 when using the `DrawText(...)` methods.

So we know how to draw text on a image, and we know what size the text will be rendered at lets pull it all together.


```c#
using(Image img = Image.Load("sourceImage.jpg"))
{
    // firstly you are going to need a font family, Lets just grab one from the system font store.
    FontFamily family = FontCollection.SystemFonts.Find("Arial");
    // now we need to get a particularly styled/sized version 
    Font font = new Font(family, 100f, FontStyle.Regular);
    TextMeasurer measurer = new TextMeasurer();
    // we can now get the dimensions of the bounding box of a piece of text
    Size size = measurer.MeasureText("Copyright Person Name", font, 72); 
    //  calculate the scaling factor we need to change the fontsize by to fit the image
    float scalingFactor = Math.Min(image.Width / size.Width, image.Height / size.Height);
    // create a new font, based on the current one with the size scaled
    Font scaledFont = new Font(font, scalingFactor * font.Size);
    // grey with 50% opacity
    Color fill = new Color(128, 128, 128, 128);
    // draws "Copyright Person Name" using Arial at 10pt at the top left of the image.
    img.DrawText("Copyright Person Name", scaledFont, fill, new Vector2(0,0))
}

```
Now what lets see what effect that has on our 2 images:

[![Large Image with scaled text overlay]({{ site.url }}/assets/posts/2017-04-08-watermarks/resized_large_scaled.jpg)](({{ site.url }}/assets/posts/2017-04-08-watermarks/large_scaled.jpg))

[![Small Image with scaled text overlay]({{ site.url }}/assets/posts/2017-04-08-watermarks/resized_small_scaled.jpg)](({{ site.url }}/assets/posts/2017-04-08-watermarks/small_scaled.jpg))

There we have it, our copyright overlay now fill the image and is never cropped off, it scales up on our large image and scales down on the smaller one. You can find a version of the code in this post at [SixLabors/Demos/WaterMarkSample](https://github.com/SixLabors/Demos/tree/master/WaterMarkSample) on GitHub.
