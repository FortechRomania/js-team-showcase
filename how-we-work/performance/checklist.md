# Performance Checklist

## Introduction

We see performance as an integral part of the quality of the software that we build. There's no need to re-emphasize the importance of performance in the modern web. We strongly belive that it is our duty to provide to our users a slick and fast UX, so we try to include performance optimizations in our regular working process.

Here are a couple of areas that revolve around web performance. They will be later grouped into **front-end**, **back-end** and **tooling**, but for now let's look at where we can actually improve the performance of our web applications.

* [Optimizing Critical Rendering Path](#optimizing-critical-rendering-path)
* [Keeping the bundle size to a minimum](#keeping-the-bundle-size-to-a-minimum)
* [Image Optimization](#image-optimization)
* [Interactivity and Animations](#interactivity-and-animations)
* [Backend & Server Optimizations](#backend-optimizations)
* [Performance Tests and Tools](#performance-tests-and-tools)

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

Further reading on [3rd party JS optimization](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/)

## Keeping the bundle size to a minimum

#### Minify JS and CSS
Make sure you also minimize CSS, especially since that CSS will always delay the initial render.

#### Tree shaking
When [using webpack](https://webpack.js.org/guides/tree-shaking/), make sure you disable module transpilation, so webpack can automatically do tree shaking based on ES Modules syntax.

#### Code splitting
If you bundle size is still large, one option is to split chunks of your code and lazy load them only when you need them. This is very easily done with the [dynamic import syntax and webpack](https://webpack.js.org/guides/code-splitting/). Further more, when using React, you can use [react-loadable](https://github.com/jamiebuilds/react-loadable) to abstract the complexity of the dynamic module import.

#### Eliminate seldomly used dependencies
Make sure you're using a good chunk of a library if you import it in your code. Otherwise you will end up with a lot of unused code in your final bundle that might not be easily tree shaken because of the way in which the library is built. A few examples:
* Prefer the native array functions instead of adding lodash for a few operations
* Avoid using moment.js (69 kB minified + gziped!) or make sure you don't load all locales for it.
* Create your custom components if your use case is very limited compared to a fully featured component.

#### Other ideas to help minimize the bundle size
* Use [babel-preset-env](https://github.com/babel/babel/tree/master/packages/babel-preset-env) + [browserslist](https://github.com/browserslist/browserslist) to specify browser support and limit polyfills
* Use [bundlesize](https://github.com/siddharthkp/bundlesize) in your CI to define hard size limits for your bundle.
* Generate and inspect bundle size with [webpack bundle analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer) or other similar tools
* Measure code coverage with **Chrome DevTools**

## Image Optimization
A few practices to improve the performance on website that rely heavily on images
* Defer image loading based on their importance / visibility
* Serve images according to screen size - you don't need a 1080p image on a mobile device.
* Use modern encoding formats when possible, like [Webp](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)
* Inline small images as SVGs
* Don’t render offscreen images, use IntersectionObserver to determine if the image should be fetched

## Interactivity and Animations
After optimizing the critical rendering path and the initial render, it's time to look at how the user interacts with your application. Using the following practices will help you maintain your rendering at 60fps:
* Use [passive event listeners](https://developers.google.com/web/updates/2016/06/passive-event-listeners)
* Use *opacity* and *transforms* to create css animations, avoiding unnecessary reflows.
* Use [will-change](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change) when you know element will be animated
* Constantly check performance with the Chrome DevTools Audit tab.

## Backend Optimizations
And a few tips to use on the backend and the server to help the web app performance overall:
* Don’t rely on ORMs for performant queries
* Use indexes on all columns you query
* Use pagination for long lists
* Rely on server caching when possible
* Use http/2
* Use gzip/deflate
* Rely CDNs to deliver assets (js, css, images) based on region and availability

## Performance Tests and Tools
Finally, some tools that help you on the way:
* Google lighthouse (performance, seo, accessibility, etc.)
* Google devtools / performance tab
* GTMetrix (loading times, performance charts)
* Locust.io (load testing, requires some python knowledge)
* jmeter (load testing)

## Further Reading
[Frontend Performance Checklist 2018](https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/)
