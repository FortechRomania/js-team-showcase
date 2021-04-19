## React

### Introduction
Start with [Pete Hunt's HowTo on GitHub](https://github.com/petehunt/react-howto) to understand the context of React.

Follow the ["Start Using React to Build Web Applications" tutorial on egghead.io](https://egghead.io/courses/start-using-react-to-build-web-applications) to get a good grasp of the major features of React. 

Also [on egghead, Kent Dodds' "Learn React Fundamentals and Advanced Patterns"](https://blog.kentcdodds.com/learn-react-fundamentals-and-advanced-patterns-eac90341c9db), is a good reference for beginner and advanced usages for React.

Also check this article on [engineering.opsgenie.com, "I wish I knew these before diving into React"](https://engineering.opsgenie.com/i-wish-i-knew-these-before-diving-into-react-301e0ee2e488) before you get started.

You can also follow this [react training by Alex Moldovan](https://github.com/alexnm/react-training) material, which covers all topics you should get familiar with regarding React.

Exercise: Re-write your image slider using React.

### Movie catalog app
At this stage you should start building your own application. We recommend a movie catalog app, but feel free to decide for yourself if you think something works better for you.

At this step you should have these functionalities:
* Display list of movies
* Search for a movie based on title/description
* Infinite scroll pagination
* Integrate with an API to fetch the movies

### React Router
At this step we're adding react router in the mix to create multiple pages and replicate the model of existing web sites.

Follow the [official documentation](https://reacttraining.com/react-router/) and this tutorial ["A simple React Router - v4 tutorial on Medium](https://medium.com/@pshrmn/a-simple-react-router-v4-tutorial-7f23ff27adf).

You should have the following pages:
* Home page
* Movie List (including search and pagination functionalities)
* Movie Detail Page

Additionally, you should integrate your React slider component on the home page.

### Redux
At this step we are separating our application state and the business logic from our React components.

Understand the pattern behind redux by checking out egghead's lesson on ["JavaScript Redux - the single immutable state tree](https://egghead.io/lessons/javascript-redux-the-single-immutable-state-tree).

You should enhance your application by:
* Adding redux to keep the application state
* Adding a watchlist functionality with its own page

Additionally, you should read more about [redux middlewares](http://redux.js.org/docs/advanced/Middleware.html), one of the best ways of enhancing redux and specifically about [redux-thunk](https://github.com/gaearon/redux-thunk).

In order to actually fully understand redux, one good example is to [write it from scratch](https://gist.github.com/alexnm/f696f9b627f77a3715f70192518ca5d8) (in a minimal version).

### React patterns
There are a couple of useful patterns in React which should be studied in detail:
* [Pure component](http://reactpatterns.com/#stateless-function)
* [Container component](http://reactpatterns.com/#container-component)
* [Conditional rendering](http://reactpatterns.com/#conditional-rendering)
* [High order components](https://www.sitepoint.com/react-higher-order-components/)
* [Render prop](https://reactrocket.com/post/turn-your-hocs-into-render-prop-components/)

### Advanced topics
Now that you have a good understanding of the React ecosystem, here are a couple of directions to follow:
* Implement a login functionality in your application
* Create a high order component for authenticated routes
* Check out the proposal for structuring a [large application with redux](https://github.com/alexnm/re-ducks)
* Write unit tests for your components using [enzyme](https://github.com/airbnb/enzyme)

### Recommended time
This module should take 4 to 5 weeks of learning and practicing.

### Measurable progress
At the end of this module you should be familiar with the React ecosystem and you should be able to work on a small-medium size application with React and Redux without considerable support.
