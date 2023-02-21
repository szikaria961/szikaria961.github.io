---
layout: post
title: "Why You Should Use The Image Component in Next.js"
description: "Demonstrating the benefits of the Next.js Image Component."
date: 2023-02-20
tags: [nextjs,image,tailwindcss,reactjs,example]
comments: true
share: true
---
# Why You Should Use The Image Component in Next.js
The Next.js `Image` component has some wonderful benefits. In this blog, we'll take a look at some of it's features and how it can improve our apps significantly.

To follow along with this tutorial, setup the example project:
```bash
git clone https://github.com/szikaria961/image-rendering-example.git
cd image-rendering-example
yarn install
yarn run dev
```

## What is Next.js?

Next.js is a front-end framework created by Vercel which works with React. Next.js enables server-side rendering, which allows us to load web pages extremely fast resulting in a more user-friendly experience. Today, we'll learn how the `Image` component aids in this process. Feel free to learn more about Next.js [here](https://next.js.org).

## Why should we care?

Images are the largest resources that need to be rendered during page-load on any website. If the images aren't rendered correctly our load time is much longer. Next.js offers a way to reduce page-load time with efficient image rendering. Here are some things that the image component provides:

* Improved performance
* Compressed images
* Lazyloading (only images in the viewport are rendered)
* Auto-resized images that match the max height/width of your device

## Lets start working with our example code

Open up the example app and click on the `Image Collection` button.

We'll first use our traditional HTML `<img>` element and observe it's performance using our sample image.

```typescript
import React from 'react';

function ImageCollection() {
  return (
    <div>
      <img src="https://res.cloudinary.com/sabazikaria/image/upload/v1610548592/sample.jpg" />
    </div>
  )
}

export default ImageCollection;
```


Lets inspect the image (I'm using Chrome). Go to the `Network` tab, `disable cache`.

Notice the Type (jpeg), Size (120KB) and the time (26ms, yours could be different depending on your internet speed) it took to render the image. That's quiet fast.

![](https://res.cloudinary.com/sabazikaria/image/upload/v1676910095/rdrn1vrf1kzbaosaeizu.png)

Now, let's add our `Image` component:

```typescript
<Image src="https://res.cloudinary.com/sabazikaria/image/upload/v1610548592/sample.jpg" height={1080} width={1920} />
```

When we run the above code, we get the following error:

![](https://res.cloudinary.com/sabazikaria/image/upload/v1676910996/jdzczdyufzoxrhpkzfnj.png)

We have to whitelist `res.cloudinary.com` so we can allow image compression from this domain. This restriction exists so we don't potentially open up our app to malicious activity.

Let's go to our `next.config.js` file and add our domain.


```javascript
/** @type {import('next').NextConfig} */
module.exports = {
  reactStrictMode: true,
  images: {
    domains: ['res.cloudinary.com'],
  },
  experimental: {
    appDir: true,
  },
}
```


Restart your server.

![](https://res.cloudinary.com/sabazikaria/image/upload/v1676912196/rnltgsyak4eyqfa7mkip.png)

Now the type is webp, size dropped from 120KB to 46.3KB and the time it took to render the image went from 48ms to 7ms. That's a lot faster, smaller in size and the quality of the image is identical.

There you have it! To learn more about the Next.js `Image` component, go [here](https://nextjs.org/docs/basic-features/image-optimization).
