---
layout: post
title: "Handling Configs in Node Using The Twelve-Factor App Methodology"
description: "Using dotenv to set environment configs in a node app."
date: 2020-11-27
tags: [dotenv, env, config, twelve-factor, node]
comments: true
share: true
---

## What is a Twelve-Factor App?

[Twelve-Factor](https://12factor.net/) is a methodology for building SaaS platforms or web applications suggested by developers to create a smooth experience for anyone managing, deploying or building the app.

In this post, we will be focusing on one factor of the Twelve-Factor App: [config](https://12factor.net/config).

We will do this using a node/express webserver application that shows how you can separate configuration variables and the benefits of doing so.

## Config

Configurations (configs) are a central part of any application, specifically where there is a need to support multiple environments, clients or third-party integrations. Some of the app configs include:

- Database connection properties
- [Backing service](https://12factor.net/backing-services) credentials and connection information
- Application environment specific information such as HOST (IP, Port, etc.)

To demonstrate this, we will be using an example project which can be found [here](https://github.com/introspective-code/fullstack-js-lessons/tree/master/lesson-env-config).

In our example, we’ll just use a fake `API_KEY` and `PORT` number as our configs. We will NOT store these values as hardcoded constants in our code because we want to separate our configs from our codebase.

We will be using the `dotenv` package which can be installed like so:

```
npm install dotenv
```

The **dotenv** module loads environment variables from a `.env` file into the globally accessible `process` variable in node inside `process.env`. This lets us access those variables right inside our code through a procedure that is independant of our codebase.

The following example app uses dotenv like so:

##### _`index.js`_
```javascript
...
require('dotenv').config();
...
```

In addition to that, we have a separate file inside our root project directory named `.env` where all of the environment variables are listed. We have also added `.env` to our `.gitignore` file.

##### _`.env`_
```
API_KEY=12345
PORT=8000
```

##### _`.gitignore`_
```
.env
```

Now when we put all these together into our simple express application, we can access those environment variables like so:

##### _`index.js`_
```javascript
const express = require('express');
require('dotenv').config();

const app = express();

const API_KEY = process.env.API_KEY;
const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Listening on port ${PORT}`);
});

app.get('/', (req, res) => {
  res.send(`This is my API KEY: ${API_KEY}`);
});
```

When you run this project using `npm start` and load `http://localhost:8000` in your browser, you should see:

```
This is my API KEY: 12345
```

This shows how you can invoke your environment variables using dotenv while maintaining separation between your codebase and environment configs. The idea is that our code remains the same regardless of wherever our app is being deployed and the only things that vary are our configurations.

A good rule of thumb is to ask yourself: Can we make our code open source without compromising any credentials?
