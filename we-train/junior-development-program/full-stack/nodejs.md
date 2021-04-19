## Node.js

### Introduction
Read about Node.js [on their official website, nodejs.org](https://nodejs.org/en/).
This [Node JS Tutorial by airpair.com](https://www.airpair.com/javascript/node-js-tutorial) shows how can you start working with it.

We highly recommend to practice node features on several tutorials offered by the [nodeschool](https://nodeschool.io/#workshoppers).
Check out the following workshops:
* ["Learn your node"](https://github.com/workshopper/learnyounode)
* ["How to npm"](https://github.com/workshopper/how-to-npm)

#### API Reference Documentation
The API reference documentation provides detailed information about functions and objects in Node.js. Details can be found at [https://nodejs.org/api/](https://nodejs.org/api/).

#### ECMAScript2015/ES6 Features
Check out on [ES6's docs on nodejs.org](https://nodejs.org/en/docs/es6/) how the new features from ECMAScript are enabled by default in Node.js.

#### Node.js Modules
This [article](https://team.goodeggs.com/export-this-interface-design-patterns-for-node-js-modules-b48a3b1f8f40) about what are node modules, how and/or when to write them and what are the benefits of using them. This [presentation](https://darrenderidder.github.io/talks/ModulePatterns/#/1) contains more code examples that might help in understanding this concept.

#### Recap: Async JavaScript
If you want to have a good understanding of the Node ecosystem here are a couple of features that you should know about:
* [Promises - nodeschool](https://github.com/stevekane/promise-it-wont-hurt)
* [Async/Await](https://blog.risingstack.com/mastering-async-await-in-nodejs/)
* [Generator functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function%2A). Check out [co - an npm package](https://www.npmjs.com/package/co) if you want to put it into practice.

### Express
There are several frameworks that are built over Node.js.
On [nodeframework.com](http://nodeframework.com/) you can find a list of the most popular ones.
Check out this article on [airpair.com - NodeJS Framework Comparison](https://www.airpair.com/node.js/posts/nodejs-framework-comparison-express-koa-hapi) for the comparison of three of them. As a team, we used most Express.

Practice with the node school workshop on [Express](https://github.com/azat-co/expressworks).

#### Installation
Follow the [official documentation](https://expressjs.com/en/starter/installing.html) to add Express to your project.

#### Understand Routing
General information about Node.js routing can be found on [Academind's YouTube Channel](https://www.youtube.com/watch?v=tiMLxUKrB-g). In Express is rather similar - read about it on the [official website](https://expressjs.com/en/guide/routing.html).
This article on [scotch.io](https://scotch.io/tutorials/learn-to-use-the-new-router-in-expressjs-4) might help you also understand the whole routing process.

#### The purpose of middlewares
Middlewares are functions that have access to the request, response object and the next function in the application's request-response cycle. This functions are invoked in the order they are added and they are mostly used to keep the application's code as simplified as possible.

Read more about the usage, purpose and advantages of middlewares on [expressjs official website](https://expressjs.com/en/guide/using-middleware.html)

Play around with a few middlewares:
* [Cookie parser](https://www.npmjs.com/package/cookie-parser)
* [Body parser](https://github.com/expressjs/body-parser)

#### Express best practices
This is a [great resource that covers several practices for expressjs](https://expressjs.com/en/advanced/best-practice-performance.html):
* compression
* logging
* error handling
* process management

### MongoDB and Mongoose
[MongoDB](https://docs.mongodb.com/manual/) is an open-source, document based database. The guys from [nodeschool](https://nodeschool.io) have an interesting [tutorial on Evan Lucas' GitHub account](https://github.com/evanlucas/learnyoumongo) on how to start working with it.

[Mongoose](http://mongoosejs.com/) is a tool built over MongoDB that is used for object modeling and validation. To work with it we recommend to check out this tutorial on [scotch.io](https://scotch.io/tutorials/using-mongoosejs-in-node-js-and-mongodb-applications) or this other one on [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose) tutorials. You can use the [validation resource from mongoose](http://mongoosejs.com/docs/validation.html) to see how model validation is done. Also you can play around with [queries](http://mongoosejs.com/docs/queries.html).

### Building an API from scratch
At this step you should be starting practicing by building your own API with Node.js.
The easiest way to do that is to use the [Express framework](https://expressjs.com/) and [MongoDB](https://docs.mongodb.com/manual/installation/).

In [our node starter project](https://github.com/FortechRomania/node-starter) you can find an application skeleton for a typical Node.js app. Clone the repository, install everything (do not forget the database) then start adding your code.

In [our express mongo example project](https://github.com/FortechRomania/express-mongo-example-project) you can find another skeleton for a Node.js app. The steps are the same: clone the repository, install everything and start writing your code.

If you take a look on both repositories the structure of the project is slightly different. Depending on how complex is your app you might use one or the other. The first one is used for smaller applications i.e. applications that have a small number of models and controllers. The second structure is preferred for applications that have a bigger complexity where the applications has to be properly modularized for maintenance purposes.

#### Movie catalog app
At this stage you should start building your own application. We recommend a movie catalog app, but feel free to decide for yourself if you think something works better for you.

This app has the purpose of keeping track of movies. The app should contain the following functionalities:
* Admin can login.
* The admin can add/upload the initial list of movies.
* Users can sign in.
* Users can login.
* An user can add other movies.
* An user can rate a movie.
* An user can logout.
* An user can delete its account.

Keeping in mind the functionalities mentioned above, you should have these files in you app folder:
* Express + MongoDB configuration
* A file that contains the app's routes
* App models (e.g. admin, user and movie)
* App controllers (e.g. userController.js and movieController.js)
* Middlewares (e.g. to validate an user/movie already exists)

### Recommended time
This module should take 3 to 5 weeks of learning and practicing.

### Measurable progress
At the end of this module you should be familiar with the Node.js ecosystem and you should be able to work on a small-medium size API.
