## Angular

### Some prerequisites
* Typescript - [The missing intro](https://toddmotto.com/typescript-the-missing-introduction)
* RxJs - [The missing intro](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754/)

### Introduction

Go through the following topics in order to get a grasp of the building blocks of an angular application and to get familiar with the specific syntax: 

* [Arhitecture](https://angular.io/guide/architecture)
* [Displaying data](https://angular.io/guide/displaying-data)
* [Template Syntax](https://angular.io/guide/template-syntax)
* [Lifecycle-hooks](https://angular.io/guide/lifecycle-hooks)
* [Component interaction](https://angular.io/guide/component-interaction)
* [Component style](https://angular.io/guide/component-styles)
* [Attribute directives](https://angular.io/guide/attribute-directives)
* [Structural directives](https://angular.io/guide/attribute-directives)
* [Pipes](https://angular.io/guide/pipes)
* Angular Forms
    * [User Input](https://angular.io/guide/user-input)
    * [Template drive forms](https://angular.io/guide/forms)
    * [Reactive forms](https://angular.io/guide/reactive-forms)
    * [Form Validation](https://angular.io/guide/form-validation)
* Angular [modules](https://angular.io/guide/ngmodule)
* Dependency injection
    * The [pattern](https://angular.io/guide/dependency-injection-pattern)
    * DI in [angular](https://angular.io/guide/dependency-injection)

* [Http Client](https://angular.io/guide/http)
* [Routing and navigation](https://angular.io/guide/router)

Exercise: Follow [this](https://angular.io/tutorial) tutorial to build a Heroes App.

Exercise: Build your own application. We recommend a movie catalog app, but feel free to decide for yourself if you think something works better for you.

At this step you should have these functionalities:
* Display list of movies
* Search for a movie based on title/description
* Infinite scroll pagination
* Integrate with an API to fetch the movies

### Angular patterns
There are a couple of useful patterns in Angular which should be studied in detail:
* [Stateful and stateless components](https://toddmotto.com/stateful-stateless-components)
* Observable data services [a blog post](https://blog.angular-university.io/how-to-build-angular2-apps-using-rxjs-observable-data-services-pitfalls-to-avoid/) or the `Data Architecture with Observables and RxJS` chapter from the [Ng-book](https://www.ng-book.com/2/)

You should enhance your application by: 
* Making the movie list component the only stateful component and keep the rest as stateless components
* Upgrade your services to use Behavior Subjects
* Adding a Watchlist functionality with its own page

### Advanced topics
* Check out the official angular [style guide](https://angular.io/guide/styleguide) for everything from naming convetions to a suggested application structure 
* Read about testing components and services in this [guide[(https://angular.io/guide/testing)

You could further enhance your app by:
* Restructuring to have a movie feature folder, a core folder and a shared folder
* Write tests for your component and services

### Recommended time
This module should take 4 to 5 weeks of learning and practicing.

### Measurable progress
At the end of this module you should be familiar with the Angular framework should be able to work on a small-medium size application without considerable support.
