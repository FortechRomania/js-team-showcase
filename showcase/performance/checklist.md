# Performance Checklist

## Introduction

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

## Optimizing Critical Rendering Path

When we talk about the Critical Rendering Path, or CRP, we refer to the initial load time of a web application. We ask a few questions:
* How fast does the user see something?
* How fast does the user see something relevant?
* How fast can the user interact with the page?

All these are important but if we focus on the rendering part and on the moment when the users sees the relevant content, then optimizing CRP is about shortening the delay of the [first meaningful paint](https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint). A few points to consider are:

#### Use Server Side Rendering
Modern JS frameworks (Angular, React, Vue) support server side rendering, allowing the application to become **universal**. Here's a guide to implement [server side rendering in React](https://medium.freecodecamp.org/demystifying-reacts-server-side-render-de335d408fe4). SSR minimizes the time you wait for the first meaningul paint because your components render on the server and the client only needs to load HTML and CSS. This also ensures that we can defer loading javascript files.

#### Defer JavaScript execution
If the user doesn't need JavaScript to see the initial render, we can use the `defer` attribute on script tags.
```html
<script type="text/javascript" src="/app.bundle.js" defer/>
```

Further reading on [`defer` and `async`](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html).

#### Preload critical resources
Defering resource execution is one thing, but in certain scenarios you may want to **preload** resources that you know will be used in the initial render. [Link Preload](https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content) is a nice feature that you can include in your `<head>` tag. Normally you would preload: styles, fonts or even scripts, based on how fast you need them during the initial render phase.

An example would be
```
<link rel="preload" href="/app.bundle.css" as="style">
<link rel="preload" href="/fonts/roboto.woff2" as="font" type="font/woff2" crossorigin />        
<link rel="preload" href="/app.bundle.js" as="script" />
```

#### Inline above-the-fold CSS
In order to avoid a roundtrip to fetch the initial css, there are certain scenarios in which you can inline the styles needed to render the initial screen. The browser only needs the styles which are *above-the-fold*, or inside the user viewport. There are multiple tools that help you extract above the fold css:
* [Critical](https://github.com/addyosmani/critical)
* [CriticalCSS](https://github.com/filamentgroup/criticalCSS)

#### Limit number of DOM nodes
Make sure you don't introduce too many nodes in your HTML, try to keep it clean and neat. Google Lighthouse suggests limiting your DOM Nodes to ~1500 per page.

#### Delay 3rd parties
Anything from Google Analytics to Helpdesk or other 3rd party services you are using in your website tend to delay the initial render if they are not properly delayed. Ideally, you should make sure all 3rd parties have the lowest priority for downloading and execution.

## Keeping the bundle size to a minimum

#### Minify JS and CSS
Make sure you also minimize CSS, especially since that CSS will always delay the initial render.

#### Tree shaking
#### Code splitting
#### Eliminate seldomly used dependencies
#### Use browserlist to specify support and limit polyfills
#### Use bundlesize in your CI
#### Generate and inspect bundle size with webpack bundle analyzer

## Image Optimization

#### Defer image load
#### Serve images according to screen size
#### Use modern encoding formats when possible
#### Inline small images
#### Don’t render offscreen images

## Interactivity and Animations

#### Use passive event listeners
#### Use opacity and transforms to create css animations
#### Use will-change when you know element will be animated
#### Check framework performance with DevTools Audit

## Backend Optimizations

#### Don’t rely on ORMs for performant queries
#### Use indexes on all columns you query
#### Use pagination for long lists
#### Rely on server caching when possible

## Server Optimizations

#### Use http/2
#### Use gzip/deflate

## Performance Tests and Tools

#### Google lighthouse
#### Google devtools / performance tab
#### GTMetrix
#### Locust.io
#### jmeter

## Further Reading
[Frontend Performance Checklist 2018](https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/)
