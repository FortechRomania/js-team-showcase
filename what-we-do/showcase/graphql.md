# GraphQL

### Getting Started with GraphQL
Before jumping into GraphQL you must understand what it is and that it comes as an alternative to traditional REST APIs. One important note is that GraphQL is not tied to any specific language or framework. It is just a protocol used for communicating between clients and servers.
* [Understand what GraphQL is about](https://dev-blog.apollodata.com/the-basics-of-graphql-in-5-links-9e1dc4cac055)
* Check the [official documentation](http://graphql.org/learn/) for basic concepts
* Build your first server following [this egghead course](https://egghead.io/courses/build-a-graphql-server)

### GraphQL and Mongo
Once you've built your first GraphQL server you can check this article with a nice and simple example on how to connect the `query` and `mutation` resolvers to a Mongo database.
* [Using GraphQL with MongoDB](https://www.compose.com/articles/using-graphql-with-mongodb/)

### GraphQL and Apollo
This 6-part article is a great reference to start building a React app powered by a GraphQL backend. **Apollo** is an easy-to-use client for GraphQL which allows you to write queries and mutations on any frontend application in order to communicate with a GraphQL endpoint. This series of articles goes through the basic functionalities exposed by **React-Apollo**, the library used for connecting React apps to GraphQL.
* [Getting started with React-Apollo](https://dev-blog.apollodata.com/full-stack-react-graphql-tutorial-582ac8d24e3b)

**Notes**

Be aware that GraphQL and Apollo are at new versions at the moment so setup might be a bit different. Took me a while to figure out exactly how to do it. The recommended approach is to visit the [oficial documentation](https://www.apollographql.com/docs/react/basics/setup.html) for setting up `React-Apollo`.

The suggested way for first time users is
```
npm install apollo-client-preset react-apollo graphql-tag graphql --save
```

And then 

```javascript
import { graphql, ApolloProvider } from "react-apollo";
import ApolloClient from "apollo-client";
import gql from "graphql-tag";
import { HttpLink } from "apollo-link-http";
import { InMemoryCache } from "apollo-cache-inmemory";

const client = new ApolloClient( {
    link: new HttpLink( { uri: "<link to graphql endpoint>" } ),
    cache: new InMemoryCache( ),
} );
```

Also, keep in mind that you to set your express server to allow cross-origin requests since the backend and the frontend will run on different ports. You can easily to that with the `cors` package in express.

```
const cors = require( "cors" );

server.use( "*", cors( { origin: "http://localhost:3000" } ) );
```

Also please note that when adding **subscriptions**, the interface of the `apollo client` setup is changed drastically. You can follow the [example code from this repo](https://github.com/alexnm/graphql-playground) that I created to make it work. You can easily follow the [official documentation](https://www.apollographql.com/docs/react/features/subscriptions.html) also.

The rest of the code is similar with what is described in the article.

Also worth reading while getting deeper into React-Apollo:
* [Caching](https://www.apollographql.com/docs/react/features/caching.html)
* [Optimistic UI](https://www.apollographql.com/docs/react/features/optimistic-ui.html)
* [Using Fragments](https://www.apollographql.com/docs/react/features/fragments.html)

### Demo

[Here is a demo app](https://github.com/alexnm/graphql-playground) I built using the major features of `GraphQL`.

### Further reading

* [Getting started with React and Apollo](https://www.howtographql.com/react-apollo/1-getting-started/)
* [Building a real-time chat with GraphQL](https://blog.graph.cool/how-to-build-a-real-time-chat-with-graphql-subscriptions-and-apollo-d4004369b0d4)
* [Using Vue with Apollo](https://medium.com/yld-engineering-blog/using-vue-with-apollo-65e2b1297592)
