The purpose of this page is to provide a brief overview of unit and end to end testing solutions used within one of our projects.

##Unit testing
For unit and component testing, we are using:
* [phantomjs] (http://phantomjs.org/) - headless WebKit
* [mocha] (https://mochajs.org/) - test framework running on node and in browser (mocha-phantomjs used to run tests in browser)
* chai - assertion library
* sinon - stubs & mocks
* [browserify] (http://browserify.org/) - bundle up modules
* [Istanbul] (https://github.com/gotwarlost/istanbul) - code coverage reports

**Packages used:**
* gulp-mocha
* gulp-mocha-phantomjs
* chai
* sinon
* browserify
* browserify-istanbul
* gulp-istanbul
* gulp-istanbul-report

Due to the fact that tests are run in PhantomJs, gulp-istanbul-report is needed to generate coverage reports. In order to have coverage working within browserify and Istanbul, we use browserify-istanbul.

##End to end testing
For end to end testing on native mobile apps (web view), we are using:
* [appium] (http://appium.io/)
* [webdriver.io] (http://webdriver.io/)
* [mocha] (https://mochajs.org/)
* chai
* [sauceLabs] (https://saucelabs.com/enterprise#automated-testing-platform) - cloud based platform for automated web and mobile testing

For end to end testing on web, we are using: 
* [testcafe] (http://devexpress.github.io/testcafe/)
* [sauceLabs] (https://saucelabs.com/enterprise#automated-testing-platform) - cloud based platform for automated web and mobile testing

Previously, instead of test cafe we were using web driver.io + mocha.

**Testcafe**
*Installation*
1st option: TestCafe Github: https://github.com/DevExpress/testcafe
run npm install -g testcafe

2nd option: TestCafe official website: https://testcafe.devexpress.com/
Download TestCafe for your current OS & Install

*Running test with TestCafe*
testcafe chrome tests/
Runs all file tests that are inside the folder “tests/”. The tests are done on the currently installed version of Chrome Browser.

testcafe safari tests/
Runs all file tests that are inside the folder “tests/”. The tests are done on the currently installed version of Safari Browser.

testcafe firefox tests/
Runs all file tests that are inside the folder “tests/”. The tests are done on the currently installed version of Mozilla Firefox Browser.

testcafe all tests/
Runs all file tests that are inside the folder “tests/” on all locally installed browsers. The tests run in parallel.

testcafe "chrome:emulation:device=iphone 6" tests/test.js
or
testcafe "chrome:emulation:width=100;height=200;mobile=true;orientation=vertical;touch=true" tests/test.js
Runs tests in Chrome's built-in device emulator

testcafe remote --qr-code test/test.js
Generates qr code that can be used on several devices ( both desktop and mobile )

*Integration with SauceLabs*
Install the plugin that integrates TestCafe with SauceLabs Testing Cloud -  created by Developer Express Inc. (https://devexpress.com) - testCafe owners
npm install testcafe-browser-provider-saucelabs

More info on: https://www.npmjs.com/package/testcafe-browser-provider-saucelabs
Set Environment Variables for Authentication Credentials. More details here.
Open Terminal mode, enter vi ~/.bash_profile, and then press Enter.
Press i to insert text into your profile file.
Enter these lines:

export SAUCE_USERNAME="your Sauce username"
export SAUCE_ACCESS_KEY="your sauce access key"

Press Escape.
Hold Shift and press Z twice (z z) to save your file and quit vi.
In the terminal, enter source ~/.bash_profile.

To determine the available browser aliases by running:
testcafe -b saucelabs

To run on an emulated device:
testcafe "saucelabs:Android Emulator Tablet@4.4" './test/testjs'

To run on more emulated devices just chain the name of the desired devices:
testcafe "saucelabs:iPhone 6 Plus Simulator@9.3","saucelabs:Android Emulator Tablet@4.4" './test/test.js'


**Resources**
[Testcafe Features](https://vs.componentsource.com/product/testcafe/features)
[Test api](http://devexpress.github.io/testcafe/documentation/test-api/)
[Testcafe browsers support](http://devexpress.github.io/testcafe/documentation/using-testcafe/common-concepts/browser-support.html)
[How to use testcafe with saucelabs](https://www.devexpress.com/Support/Center/Question/Details/T119616/testcafe-how-to-use-saucelabs)
[Testing browser with gulp and phantoms](http://blog.silicak.es/2016-07-07-testing-browser-gulp-phantomJS-mocha-istanbul)

**Saucelabs**
[Pricing](https://saucelabs.com/pricing)
[Platform Configurator](https://wiki.saucelabs.com/display/DOCS/Platform+Configurator#/)
*automated testing on emulators only
*versions available > IOS 8.1, Android 4.4
*CI integration

**AWS Device Farm**
[Pricing](https://aws.amazon.com/device-farm/pricing/)
[What is it](https://docs.aws.amazon.com/devicefarm/latest/developerguide/welcome.html)
*automated testing on real mobile devices
*versions available > IOS 8.1, Android 4.1.1 ([device list](https://aws.amazon.com/device-farm/device-list/))
*CI Integration ([Jenkins](https://github.com/awslabs/aws-device-farm-jenkins-plugin/blob/master/README.md))

