---
layout: post
title: "Understanding getServerSideProps in Next.js"
description: "Learn Server-side rendering and how to implement it using getServerSideProps method in Next.js apps"
date: 2023-02-25
tags: [nextjs,serversiderendering,reactjs,example]
comments: true
share: true
---
![](https://res.cloudinary.com/sabazikaria/image/upload/v1677340490/kyjqmxv1ivdggo7j2lws.png)

## What is Server-side Rendering in Next.js

In order to understand the function `getServerSideProps`, we need to first learn what server-side rendering is. It is the process of building and rendering web pages on the server and sending them to the client as HTML. This gives us faster page load times, better user experience and better search engine optimization. Remember this can take a very long time so we have to be selective about when we use it.

## Real-world example?

Imagine we want to build a small house made of Legos. Normally, we would build the entire house and then show it to our friends. But, we don't live in a normal world. Instead, we build one room at a time and our friends can immediately see the finished rooms as we finishe them, instead of waiting for the whole house to be finished?

That's kind of like server-side rendering in Next.js!

When we visit a website, the browser normally waits for the entire website to load before showing us anything. But with server-side rendering, Next.js can build and show us parts of the website as they become available, instead of waiting for the entire website to be ready.

This means that we can see some parts of the website right away, even if other parts are still being built. It can make the website feel faster and more responsive, even if it has a lot of content. Let's jump right into coding!

To follow along with this tutorial, setup the example project:

```bash
git clone https://github.com/szikaria961/image-rendering-example.git
cd image-rendering-example
yarn install
yarn run dev
```

## What is getServerSideProps?

`getServerSideProps` is a method in Next.js that allows you to fetch data at runtime before rendering a page on the server side. It can be used to fetch data from an external API, a database, or any other data source. In our example we'll use an external API: `https://fruityvice.com/api/fruit/all`. The data we get is then made available as props to the page that is being rendered.

## Lets start working with our example code

Open up the example app and click on the `Fruits` button.

Note that our getServerSideProps method is exported and it's an asynchronous function that returns an object with the data as fruits as props to the page component. Here's an example:


```typescript
function  FruitsList({ fruits }) {
  return (
    <>
      <h1>List of Fruits</h1>
      {fruits.map(fruit => {
        return (
          <p key={fruit.id}>
            Name: {fruit.name} - Sugar: {fruit.nutritions.sugar} - Calories: {fruit.nutritions.calories}
          </p>
        )
      })
      }
    </>
  )
}

export default FruitsList;

export async function getServerSideProps() {
  const res = await fetch('https://fruityvice.com/api/fruit/all')
  const data = await res.json();

  return {
    props: {
      fruits: data,
    }
  }
}
```



We used the fetch API to fetch fruits data from an external API, and then we're returning an object with a props key that contains the fetched data as fruits. This data is available as props to the FruitList component. This technique allows us to load our fruits page faster, lower the time it takes to interact with our page resulting in a much a better user experience.

Overall, getServerSideProps provides a powerful tool for fetching data dynamically on the server side and passing that data as props to a page component in Next.js.

To see how much faster server-sider rendering is compared to client-side rendering, feel free to play around with the commented code in `FruitList` component. To learn more about getServerSideProps with Next.js, go [here](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props).
