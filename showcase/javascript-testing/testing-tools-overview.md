# Tests categories

Tests written to check software functionality can be grouped into a few categories. Some of the most popular categories include:

* unit tests: check input => output of self-contained functions.
* integration tests: check that individual pieces of your app play nicely together.
* end-to-end tests (automation): check that entire features work from the user’s perspective.

[Here](https://www.sitepoint.com/unit-test-javascript-mocha-chai/) is a brief explanation of what are unit tests and why are they good to have. 

# Tests tools

There are a couple of tools that facilitate tests writing. These can be grouped in categories as follows.

### Mocking libraries
* [Sinon](http://sinonjs.org/)
* [Js-mock](https://www.npmjs.com/package/js-mock)

### Assertion libraries: 
* [should.js](https://shouldjs.github.io/) - BDD style 
* [expect.js](https://github.com/Automattic/expect.js?files=1) - expect() style assertions
* [chai](http://chaijs.com/api/) - expect(), assert() and should-style assertions
* [better-assert](https://github.com/tj/better-assert) - C-style self-documenting assert()

### Test frameworks
* [Mocha](https://mochajs.org/) 
* [Jasmine](https://jasmine.github.io/)
* [QUnit](http://qunitjs.com/)
* [Jest](https://facebook.github.io/jest/) - has assertion, mocking, runner built-in

### Test runners
* [Karma](https://karma-runner.github.io/1.0/index.html) (test framework agnostic)

### Test "utilities"
* [Enzyme](https://github.com/airbnb/enzyme)
* [PhantomJs](http://phantomjs.org/)

### Browser automation (End-to-End tests)
* [Selenium](http://www.seleniumhq.org/)
* [Testcafe](https://testcafe.devexpress.com/)

### Automation libraries (End-to-End tests)
* Appium (http://appium.io/slate/en/master/?java#about-appium, https://github.com/appium/appium/blob/master/docs/en/about-appium/intro.md, https://www.npmjs.com/package/appium-test, https://github.com/admc/wd)
* [Webdriver.io](http://webdriver.io/)

### Cloud testing (browsers and devices providers)
* [Browserstack](https://www.browserstack.com/automate)
* [Saucelabs](https://saucelabs.com/)
* [Aws device farm](https://aws.amazon.com/device-farm/)

### Code coverage
* Instanbul

# Tests examples

Unit testing - https://github.com/ancutac/javascript-testing/blob/master/README.md

End to end testing - https://github.com/FortechRomania/js-team-showcase/blob/master/showcase/javascript-testing/end-to-end-testing.md
