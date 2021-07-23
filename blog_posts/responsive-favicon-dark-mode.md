---
title: How can I create a custom responsive favicon for dark mode?
type: question
tags: css,visual
authors: chalarangelo
cover: blog_images/dark-mode.jpg
excerpt: Learn how to create a custom responsive favicon that can adapt its color palette for dark mode with this quick guide.
firstSeen: 2020-11-27T13:25:30+02:00
lastUpdated: 2021-06-12T19:30:41+03:00
---

The rise of dark mode in recent years has made many website favicons feel awkward or even impossible to see in some cases. Provided your design team has created the appropriate assets, it's relatively easy to create a responsive favicon that can handle the user's color scheme preference without too much effort.

In order to create a responsive favicon, you need an SVG icon with as few colors as possible and two color palettes, one for light mode and one for dark mode. Usual rules about icon clarity and complexity apply, so make sure your icon meets all the necessary criteria to be visually distinguishable in any scenario. In our example, we will be using a monochrome icon from the fantastic [Feather icon set](https://feathericons.com/).

Leveraging embedded styles in SVG images and the `prefers-color-scheme` media query, we can create an appropriate `<g>` element to group all the elements of the icon and, using the `id` of the group, we can then apply the color palette for each design. Here's what our final SVG asset looks like:

```html
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
  <style>
    #icon {
      stroke: #000;
      stroke-width: 2px;
      stroke-linecap: round;
      stroke-linejoin: round;
      fill: none;
    }

    @media (prefers-color-scheme: dark) {
      #icon {
        stroke: #fff;
      }
    }
  </style>
  <g id="icon">
    <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"></path>
    <line x1="3" y1="6" x2="21" y2="6"></line>
    <path d="M16 10a4 4 0 0 1-8 0"></path>
  </g>
</svg>
```

After creating the SVG asset, you need only include the custom SVG favicon in the page's `<head>` element and you're ready to go. Be sure to include a PNG fallback, if possible, with a rendered version of the icon in either palette:

```html
<head>
  <!-- Provided you have a rendered PNG fallback named favicon.png -->
  <link rel="icon" type="image/png" href="favicon.png" >
  <!-- Provided the SVG icon is named favicon.svg -->
  <link rel="icon" type="image/svg" href="favicon.svg" >
</head>
```