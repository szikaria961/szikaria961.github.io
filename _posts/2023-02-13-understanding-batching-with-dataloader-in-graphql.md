---
layout: post
title: "Understanding Batching with DataLoader in GraphQL"
description: "Understanding why we run into performance issues with GraphQL queries and how we can leverage DataLoader to help with that."
date: 2023-02-13
tags: [dataLoader, graphql, graphql-yoga, node]
comments: true
share: true
---

If you’ve worked with graphql at a production-level or ran into poor performance with executing GraphQL queries then you’re already familiar with dataLoader. You’ll also know them if you’ve ever overloaded your database with requests. In this blog we’ll try to understand why we run into performance issues with GraphQL queries and how dataLoader can help us. We’ll first go through a naive per-field resolver pattern to track how many calls to the database we make for a simple getBooks query without dataLoader and then with dataLoader. We will be following this example code found at [github](https://github.com/szikaria961/dataloader-example). Then we’ll move on to solving the n+1 problem that comes with using GraphQL. <em>(Please see the ReadMe file for more information on how to run the queries discussed in this blog)</em>

To follow along, setup:

```
git clone https://github.com/szikaria961/dataloader-example.git
cd dataloader-example
npm install
npm run start:watch
```

## Example
Let’s say that we have the following GraphQL type definition.

##### _`schema.ts`_
```

type Query {
  book(id: ID!): Book!
  books: [Book!]!
}

type Book {
  id: ID!
  name: String!
  author: String!
  price: String!
  description: String!
}
```
We have an array of books:

##### _`books.ts`_
```
export const books: Book[] = [
  {
    id: "1",
    name: "Thinking, Fast and Slow",
    author: "Daniel Kahneman",
    price: 14.99,
    description:
      "Two systems drive the way we think and make choices, Kahneman explains: System One is fast, intuitive, and emotional; System Two is slower, more deliberative, and more logical.",
  },
  {
    id: "2",
    name: "Clean Code: A Handbook of Agile Software Craftsmanship",
    author: "Robert Martin",
    price: 46,
    description:
      "Even bad code can function. But if code isn't clean, it can bring a development organization to its knees. Every year, countless hours and significant resources are lost because of poorly written code. But it doesn't have to be that way.",
  },
];
```
Resolvers:

##### _`schema.ts`_
```
resolvers: {
    Query: {
      book: (_, { id }) => ({ id }),
      books: () => books.map((d) => ({ id: d.id })),
    },
    Book: {
      name: async ({ id }) => {
        const { name } = getBookById(id);

        return name;
      },
      author: async ({ id }) => {
        const { author } = getBookById(id);

        return author;
      },
      price: async ({ id }) => {
        const { price } = getBookById(id);

        return price;
      },
      description: async ({ id }) => {
        const { description } = getBookById(id);

        return description;
      },
    },
  },
```
Here’s our getBookById function accepts an id and finds books through our different books of array of books. Notice the console log; this will help us keep track of how many times `getBookById` gets called per query.

##### _`provider.ts`_
```
export const getBookById = (id: string): Book => {
  console.log(`Calling getBookById: ${id}`);

  return books.find((d) => d.id === id);
}
```
When I run the following query:
```
{
  books {
    id
    name
  }
}
```
this is what I see in my terminal: `getBookById` gets called two times

```
Calling getBookById: 1
Calling getBookById: 2
```
How many times do you think `getBookById` will get called if I add two additional fields to books query?
```
{
  books {
    id
    name
    price
    description
  }
}
```
Six times!
```
Calling getBookById: 1
Calling getBookById: 1
Calling getBookById: 1
Calling getBookById: 2
Calling getBookById: 2
Calling getBookById: 2
```
Can you now imagine how many more requests to the database we’ll be making if our dataset got bigger and we had nested fields in our query.

## DataLoader
This is where dataLoader comes to the rescue! We’ll create a function that allows us to pass multiple id's which can then pass onto `getBookById`. We’ll build a loading function called `getBooksByIds` which accepts an array of keys and returns a Promise that resolves to an array of book ids.

##### _`index.ts`_
```
export const getBooksByIds = async (ids: string[]): Promise<Book[]> => {
  return ids.map((id) => getBookById(id));
};
```
Now let’s instantiate a `new DataLoader`, pass our newly created `getBooksByIds` function to it and update our `Book` resolver.

##### _`schema.ts`_

```
.
.
.
import * as DataLoader from "dataloader";

const bookLoader = new DataLoader(getBooksByIds);

.
.
.
Book: {
      name: async ({ id }) => {
        const { name } = await bookLoader.load(id);

        return name;
      },
      author: async ({ id }) => {
        const { author } = await bookLoader.load(id);

        return author;
      },
      price: async ({ id }) => {
        const { price } = await bookLoader.load(id);

        return price;
      },
      description: async ({ id }) => {
        const { description } = await bookLoader.load(id);

        return description;
      },
    },
```
Let’s re-run our query and see what we get in our terminal. In our old resolver this query would have called `getBookById` eight times!
```
{
  books {
    id
    name
    price
    description
    author
  }
}
```
After adding our dataLoader, how many times do we expect the above query to hit `getBookById`?
```
Calling getBookById: 1
Calling getBookById: 2
```
Just twice!

There you have it! A simple example that demonstrates the power of dataLoader. To learn more about dataLoader, checkout: [dataLoader](https://github.com/graphql/dataloader)!
