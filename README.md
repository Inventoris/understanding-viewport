# Understanding Viewport

Let's imagine you have an Apple iPhone 14. Its resolution is 1170 × 2532 pixels. That means the screen consists of 1170 horizontal pixels and 2532 vertical pixels. So far, so simple, right?

![iPhone 14 image with dimensions](https://github.com/user-attachments/assets/2904fd37-b8e6-40e8-9de0-31dfc08e6393)

But if we take a closer look at the width and height, we’ll see that they are nowhere near the usual mobile sizes we use in the CSS `@media` directive! This is a huge screen for a smartphone — taller than desktop and similar in width to a tablet. In this case, we would expect to see a tablet layout or something like that on the relatively small iPhone screen, which would make using the site practically impossible.

![Tablet layout on small iPhone screen](https://github.com/user-attachments/assets/9cea9aab-7d40-43e0-be64-05bc5faf490a)

However, that doesn’t happen, because CSS sees completely different screen dimensions: 390 pixels wide and 844 tall. Why is that? Let's break it down.

## CSS Pixel VS Device Pixel

In the era of high pixel density screens, browsers have learned to translate the screen resolution into a CSS-friendly equivalent. Without this, we wouldn't be able to tell in the code whether we're dealing with a large monitor or a tiny Samsung smartphone screen with high pixel density.

Now, one CSS pixel on such devices — like those with Retina displays — corresponds to several real pixels. This ratio is called _Device Pixel Ratio (DPR)_. Let's break it down using the Apple iPhone 14 as an example:

|                Real Pixels                          |                CSS Pixels                 |    DPR    |
|-----------------------------------------------------|-------------------------------------------|-----------|
| 1170 x 2532                                         | 390 x 844                                 |    3x     |

So, each CSS pixel corresponds to three real pixels. This works not only with phones but with all screens. It can be confusing when we see different values in device specs and CSS, but it’s what allows modern web to function correctly.

![Real vs. CSS dimensions](https://github.com/user-attachments/assets/2095ee0a-717d-46a0-9784-c9c3a3171805)

If your monitor on a store's website has a resolution of 1920 x 1080 and _DPR_ = 1.1x, CSS will see 1746 pixels wide. It was 1920, now it’s 1746 — that’s how it works!

## Subtracting More

But that's not all. Part of the device height is reserved for various system UI elements — for mobile devices, for instance, the top bar with battery level, signal strength, etc. And when we open a website in the browser, even more pixels are subtracted for browser UI bars. Their heights vary by device, browser version, model, and orientation.

![Image showing how bars eat up viewport height and what viewport is](https://github.com/user-attachments/assets/d0762fa7-6dd4-4546-a39f-fffe69abf5df)

It’s hard to list exact bar sizes, but here's an example for the same Apple iPhone 14 in Safari: ~47 pixels (system bar) + ~134 pixels (Safari bar) = ~181 pixels lost just to bars. By the way, width can also be "eaten up", for example, by scrollbars.

So what's left after all the subtractions? That's the viewport! In other words, the part of the webpage visible to the user.

## Viewport Meta Tag

Alright, now let’s deal with one last important topic: how do we tell the page to adapt to the CSS resolution instead of the real one? For that, we use the following meta tag:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

I’m sure you’ve seen it before. Here’s what each part means:

|                     Value                     |                           Explanation                           |
|-----------------------------------------------|-----------------------------------------------------------------|
| width=device-width                            |      The viewport width should match the device’s CSS width     |
| initial-scale=1                               |      The initial page scale should be 100%                      |

So, this `viewport` meta tag with the values above tells the page: adapt to the CSS dimensions, not the real device size, and keep the scale 1:1. Thanks to it — a true web hero!

## In The End

If a device’s resolution is 1170 x 2532 pixels, that doesn’t mean the webpage will open at those dimensions. On high pixel density screens, CSS will see an equivalent — for _DPR_ = 3x, that’s 390 x 844 pixels. And with the system and browser bars, the viewport might shrink to 390 x 663 pixels.

Understanding this logic will help you avoid a ton of bugs — always consider these transformations. And now you know what the heck this viewport thing is!

> If this guide was helpful for you, give it a 🌟 and follow me for more updates!
