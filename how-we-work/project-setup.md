# Standard Project Setup

### Common
We try to approach all projects, small or large, with a consistent project setup. This includes things like [a common ESlint config](https://github.com/FortechRomania/js-team-showcase/blob/master/how-we-work/coding-guidelines.md), a common approach to npm tasks and git flows, a common folder structure. Towards the end of the document, we will go through the specific setup aspects for React/Angular or other framework centric projects.

Let's have a look at a standard `package.json` on one our our projects:
```javascript
{
  "name": "<project-name>",
  "version": "1.0.0",
  "description": "...",
  "scripts": {
    "dev": "webpack --progress --colors --watch",
    "build": "webpack --progress",
    "start": "nodemon --watch src/server.js",
    "linter": "eslint src",
    "test": "jest"
    "bundlesize": "bundlesize",
    "precommit": "npm run lint",
    "prepush": "npm run test"
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "Firefox ESR"
  ],
  "bundlesize": [
    {
      "path": "./dist/js/app.bundle.js",
      "maxSize": "170 kB"
    },
    {
      "path": "./dist/js/lib.bundle.js",
      "maxSize": "110 kB"
    }
  ],
  "dependencies": {
  },
  "devDependencies": {
    "babel": "^6.3.26",
    "babel-eslint": "^7.1.1",
    "babel-loader": "^7.1.1",
    "babel-minify-webpack-plugin": "^0.2.0",
    "babel-preset-env": "^1.6.0",
    "bundlesize": "^0.15.3",
    "eslint": "^4.8.0",
    "eslint-config-fortech": "^2.0.2",
    "eslint-plugin-compat": "^1.0.2",
    "eslint-plugin-import": "^2.7.0",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "husky": "^0.14.3",
    "jest": "^22.1.2",
    "webpack": "^3.4.1",
    "webpack-bundle-analyzer": "^2.2.1"
  }
}
```

Let's cover a few tools / libs from this setup.

#### Webpack
We use Webpack for bundling modern web applications. We also use `Uglify` or `Minify` as plugins to output production code. Additionally, we integrate [webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer) to generate more details about the bundle size and about how dependencies are composing in the production code. Finally, we add the [friendly-errors-plugin](https://www.npmjs.com/package/friendly-errors-webpack-plugin) for debugging purposes when running the project locally.

#### Babel
In order to support older browsers we transpile the code via [Babel](https://babeljs.io/). The babel settings go into `.babelrc`. In order to use babel with Webpack we rely on `babel-preset-env` which can optionally transpile code based on the `browserlist` which is found in `package.json`.

A standard `.babelrc` file:
```json
{
    "presets": [
        [ "env", { 
            "modules": false
        } ],
        "react"
    ]
}
```

Note that `modules: false` will not transpile ESModules to RequireJS, enabling webpack to tree shake your code.

#### Husky
In order to ensure stability and code quality we've come up with a standard practice of using precommit/prepush hooks to lint and test the code that ends up on the central repository. We're leveraging [husky's](https://github.com/typicode/husky) ability to simply use standard npm scripts: `precommit`, `prepush`.

#### Jest/Mocha
We don't have a strong preference for one testing tool, but recently `Jest` has gained a lot of attention. We added it on multiple projects because of the easy setup behind it and because you get all the tools in one pack.

#### ESLint
We have a common `eslint` config for all projects, with a specific flavor for `React` which supports `JSX` and other `React` specific rules. You can read more about our choices [on this repository, Coding Guidelines article](https://github.com/FortechRomania/js-team-showcase/blob/master/how-we-work/coding-guidelines.md). We run the `eslint` task on precommit hooks to make sure that only the code that respects all the standard rules ends up on the central repo.

#### Bundlesize
Finally we want to keep the size of our bundles in control. We use `bundlesize` to test against some predefined values from `package.json`. Of course these values are subject to change as the project increases in size and complexity, but it's always a good reminder that we need to control the size of the code we ship.

### React
Under construction

### Angular
Under construction
