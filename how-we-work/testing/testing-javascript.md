# Tests categories

Tests written to check software functionality can be grouped into a few categories. Some of the most popular categories include:

* unit tests: check input => output of self-contained functions.
* integration tests: check that individual pieces of your app play nicely together.
* end-to-end tests (automation): check that entire features work from the user’s perspective.

A great overview of testing and testing tools can be found on [medium.com, An Overview of JavaScript Testing in 2018](https://medium.com/welldone-software/an-overview-of-javascript-testing-in-2018-f68950900bc3).

On [sitepoint.com](https://www.sitepoint.com/sinon-tutorial-javascript-testing-mocks-spies-stubs/)'s a brief explanation about spies vs. stubs vs. mocks. In a nutshell, use: 
* Spies - if you simply want to watch and verify somethings happens in your test case.
* Stubs - if you simply want to specify how something will work to help your test case.
* Mocks - if you want to have both of the above on a single dependency in your test case.

Another great resource on testing node can be found on [hackernoon.com, Testing Node in JS](https://hackernoon.com/testing-node-js-in-2018-10a04dd77391).

# Tests tools

There are a couple of tools that facilitate tests writing. These can be grouped in categories as follows.

### Mocking libraries
* [Sinon](http://sinonjs.org/)
* [Js-mock](https://www.npmjs.com/package/js-mock)
* [Nock](https://github.com/nock/nock)
* [mock-require](https://github.com/boblauer/mock-require)

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
* Appium (http://appium.io/docs/en/about-appium/intro/, https://github.com/appium/appium/blob/master/docs/en/about-appium/intro.md, https://www.npmjs.com/package/appium-test, https://github.com/admc/wd)
* [Webdriver.io](http://webdriver.io/)

### Cloud testing (browsers and devices providers)
* [Browserstack](https://www.browserstack.com/automate)
* [Saucelabs](https://saucelabs.com/)
* [AWS device farm](https://aws.amazon.com/device-farm/)

### Code coverage
* Istanbul

# Examples

A basic JavaScript testing setup with webpack, karma, mocha, chai, sinon and istanbul can be found at [https://github.com/ancutac/javascript-testing](https://github.com/ancutac/javascript-testing)

On [sitepoint.com](https://www.sitepoint.com/unit-test-javascript-mocha-chai/) you can find another article explaining unit testing setup with mocha.

If want want to skip all the tedious configuration, you can use Jest, a testing framework with everything built in. On [https://github.com/ancutac/javascript-testing/tree/jest](https://github.com/ancutac/javascript-testing/tree/jest) is an example project setup. Since that's a branch of a previous configuration, you can check the comparison between jest setup and karma + mocha + chai + sinon + instanbul.
