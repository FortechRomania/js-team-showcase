## Performance Checklist

### Introduction

We see performance as an integral part of the quality of the software that we build. There's no need to re-emphasize the importance of performance in the modern web. We strongly belive that it is our duty to provide to our users a slick and fast UX, so we try to include performance optimizations in our regular working process.

Here are a couple of areas that revolve around web performance. They will be later grouped into **front-end**, **back-end** and **tooling**, but for now let's look at where we can actually improve the performance of our web applications.

* Optimizing Critical Rendering Path
* Keeping the bundle size to a minimum
* Image Optimization
* Interactivity and Animations
* Backend Optimizations
* Server Optimizations
* Performance Tests and Tools
* Load Tests and Tools

All these are considered in the realm of modern web development with frontend frameworks rendering complex applications and thin APIs serving the data.

### Optimizing Critical Rendering Path

When we talk about the Critical Rendering Path, or CRP, we refer to the initial load time of a web application. We ask a few questions:
* How fast does the user see something?
* How fast does the user see something relevant?
* How fast can the user interact with the page?

All these are important but if we focus on the rendering part and on the moment when the users sees the relevant content, then optimizing CRP is about shortening the delay of the [first meaningful paint](https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint). A few points to consider are:

#### Use Server Side Rendering
#### Preload critical resources
#### Inline above-the-fold CSS
#### Defer JavaScript execution
#### Limit number of DOM nodes
#### Delay 3rd parties

A few articles and references on optimizing CRP:
* coming soon

### Keeping the bundle size to a minimum

#### Minify JS and CSS
#### Tree shaking
#### Code splitting
#### Eliminate seldomly used dependencies
#### Use browserlist to specify support and limit polyfills
#### Use bundlesize in your CI
#### Generate and inspect bundle size with webpack bundle analyzer

### Image Optimization

#### Defer image load
#### Serve images according to screen size
#### Use modern encoding formats when possible
#### Inline small images
#### Don’t render offscreen images

### Interactivity and Animations

#### Use passive event listeners
#### Use opacity and transforms to create css animations
#### Use will-change when you know element will be animated
#### Check framework performance with DevTools Audit

### Backend Optimizations

#### Don’t rely on ORMs for performant queries
#### Use indexes on all columns you query
#### Use pagination for long lists
#### Rely on server caching when possible

### Server Optimizations

#### Use http/2
#### Use gzip/deflate

### Performance Tests and Tools

#### Google lighthouse
#### Google devtools / performance tab
#### GTMetrix
#### Locust.io
#### jmeter

