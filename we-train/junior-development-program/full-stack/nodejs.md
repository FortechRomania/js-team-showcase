## Node.js

### Introduction
Read about Node.js [here](https://nodejs.org/en/).
This [tutorial](https://www.airpair.com/javascript/node-js-tutorial) shows how can you start working with it.

### API Reference Documentation
The API reference documentation provides detailed information about functions and objects in Node.js. Details can be found at this [link](https://nodejs.org/api/)

### ECMAScript2015/ES6 Features
Check out [here](https://nodejs.org/en/docs/es6/) how the new features from ECMAScript are enabled by default in Node.js

### Node.js Modules
This [article](https://team.goodeggs.com/export-this-interface-design-patterns-for-node-js-modules-b48a3b1f8f40)about what are node modules, how and/or when to write them and what are the benefits of using them. This [presentation](https://darrenderidder.github.io/talks/ModulePatterns/#/1) contains more code examples that might help in understanding this concept.

### Node.js Framework: Express
There are several frameworks that are build over Node.js.
[Here](http://nodeframework.com/) you can find a list of the most popular ones.
Check out this [link](https://www.airpair.com/node.js/posts/nodejs-framework-comparison-express-koa-hapi) for the comparison of three of them. As a team, we used most Express.

#### Installation
Follow the [official documentation](https://expressjs.com/en/starter/installing.html) to add Express to your project.
#### Understand Routing
General information about Node.js routing can be found [here](https://www.youtube.com/watch?v=tiMLxUKrB-g). In Express is rather similar - read about it on the [official website](https://expressjs.com/en/guide/routing.html).
This [link](https://scotch.io/tutorials/learn-to-use-the-new-router-in-expressjs-4) might help you also understand the whole routing process.

#### The purpose of middlewares
Middlewares are functions that have access to the request, response object and the next function in the application's request-response cycle. This functions are invoked in the order they are added and they are mostly used to keep the application's code as simplified as possible.


Read more about the usage, purpose and advantages of middlewares at this [link](https://expressjs.com/en/guide/using-middleware.html)

### Practice
We highly recommend to practice node features on several tutorials offered by the [nodeschool](https://nodeschool.io/#workshoppers).
Check out the following workshops:
* ["Learn your node"](https://github.com/workshopper/learnyounode)
* ["How to npm"](https://github.com/workshopper/how-to-npm)
* [Express](https://github.com/azat-co/expressworks)
* [Promises](https://github.com/stevekane/promise-it-wont-hurt)

### More Practice - Building an API from scratch
At this step you should be starting practicing by building your own API with Node.js.
The easiest way to do that is to use the [Express framework](https://expressjs.com/) and [MongoDB](https://docs.mongodb.com/manual/installation/).


[Here](https://github.com/FortechRomania/node-starter) you can find an application skeleton for a typical Node.js app. Clone the repository, install everything( do not forget the database ) then start adding your code.


[Here](https://github.com/FortechRomania/express-mongo-example-project) you can find another skeleton for a Node.js app. The steps are the same: clone the repository, install everything and start writing your code.


If you take a look on both repositories the structure of the project is slightly different. Depending on how complex is your app you might use one or the other. The first one is used for smaller applications i.e. applications that have a small number of models and controllers. The second structure is preferred for applications that have a bigger complexity where the applications has to be properly modularized for maintenance purposes.

### Advanced topics
If you have a good understanding of the Node ecosystem here are a couple of features that you should know about:
* [Async/Await](https://blog.risingstack.com/mastering-async-await-in-nodejs/)
* [Generator functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function%2A). Use [co](https://www.npmjs.com/package/co) if you want to put it into practice.

### Recommended time
This module should take 3 to 5 weeks of learning and practicing.

### Measurable progress
At the end of this module you should be familiar with the Node.js ecosystem and you should be able to work on a small-medium size API.
