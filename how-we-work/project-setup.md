# Standard Project Setup

### Common
We try to approach all projects, small or large, with a consistent project setup. This includes things like [a common eslint config](https://github.com/FortechRomania/js-team-showcase/blob/master/how-we-work/coding-guidelines.md), a common approach to npm tasks and git flows, a common folder structure. Towards the end of the document, we will go through the specific setup aspects for React/Angular or other framework centric projects.

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
    "babel-preset-env": "^1.6.0",
    "bundlesize": "^0.15.3",
    "eslint": "^4.8.0",
    "eslint-config-fortech": "^2.0.2",
    "eslint-plugin-compat": "^1.0.2",
    "eslint-plugin-import": "^2.7.0",
    "husky": "^0.14.3",
    "jest": "^22.1.2",
    "webpack": "^3.4.1",
    "webpack-bundle-analyzer": "^2.2.1"
  }
}

```

Let's cover a few tools / libs from this setup.

#### Webpack

#### Babel

#### Jest/Mocha

#### ESLint

#### Bundlesize

#### Husky

### React
Under construction

### Angular
Under construction
