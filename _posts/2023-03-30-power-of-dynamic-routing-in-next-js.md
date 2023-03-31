---
layout: post
title: "Power of Dynamic Routing in Next.js"
description: "Creating dynamic routes in Next.js"
date: 2023-03-30
tags: [nextjs,dynamicRoute,nextjs,example]
comments: true
share: true
---

## What is Dynamic Routing in Next.js
![](https://res.cloudinary.com/sabazikaria/image/upload/v1680224713/p1oycnwfjf2rr6ke7rpp.png)
Dynamic routing refers to the process of generating pages on the fly by using the name, id or whatever unique value of the page. Instead of creating individual pages for every fruit that our API produces, we can use dynamic routing to generate pages based on their names. With Next.js, dynamic routes enable us to create pages that fetch and display content tailored to the dynamically generated URL. This way, we can serve different content for different URL paths, unlike static routes where the content remains the same for every access to the route. Therefore, dynamic routing provides us with greater flexibility in generating content for our web pages, allowing us to deliver a more personalized experience to our users and more efficient code reuse.

## Real-world example?

Let's say you're building an e-commerce website that sells different types of envelopes. Instead of creating separate pages for each type of envelope, you can use dynamic routing to generate pages based on the envelope design.

For instance, if a user navigates to "https://envelope.com/envelopes/luxury", the website can dynamically generate a page that displays information about the luxury envelope, including its name, price, description, and image.

By using dynamic routing in this way, you can easily add new products to your website without having to manually create new pages for each product. Additionally, you can customize the content of each product page to better cater to the needs and interests of your users, resulting in a more engaging and personalized user experience.

```bash
git clone https://github.com/szikaria961/image-rendering-example.git
cd image-rendering-example
yarn install
yarn run dev
```

Note: *We'll be using serverSideProps! To know more about serverSideProps, please read my previous blog.*

## Lets start working with our example code

Open up the example app and click on the `Fruits` button.

To create a dynamic route in our existing example project, we can use square brackets [] to wrap a portion of the URL path that will be dynamic.

```bash
.../pages/fruits/[name].js
```

The `name` portion of the path wrapped in square brackets indicates that it will be dynamic and can contain any value. When a user visits a URL with a path like `/fruits/apple`, Next.js will match it to this dynamic route and pass the name value as a query parameter to the `getServerSideProps` function of the page component.


```typescript
import { useRouter } from "next/router";

function FruitPage({ fruits }) {
  const router = useRouter();

  let genus, fruitName;
  const name = router.query.name;

  fruits.map(fruit => {
    if (fruit.name == name) {
      genus = fruit.genus;
      fruitName = fruit.name;
    }
  }); 
  return (
    <div>
      <h1>Fruit Name: {fruitName}</h1>
      <h3>Genus: {genus}</h3>
    </div>
  )
}

export default FruitPage;

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



We're using `useRouter` from the `next/router` module to get the current `name` of the fruit selected in our app. We then use this `name` value to get the relevant information of that specific fruit. This allows us to create dynamic pages that display appropriate information of their respective fruit based on the URL path, making our website more flexible and dynamic.

To learn more about getServerSideProps with Next.js, go [here](https://nextjs.org/docs/routing/dynamic-routes).
