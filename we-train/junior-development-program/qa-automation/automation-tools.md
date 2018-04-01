### Tools we use

## Testcafe

[Testcafe](https://devexpress.github.io/testcafe/) is a node.js tool to automate **end-to-end web testing**. You can write your Testcafe tests in **Javascript** or **Typescript** and while some may say this is not enough, we strongly disagree. Testcafe offers sollutions for any needs, except testing mobile apps. 
#### Test suites created in Testcafe can be executed:
* on any desktop browser
* on any mobile browser
* it can be integrated with Jenkins 
* it can be executed on devices from a cloud-based platform like Browserstack or SauceLabs. 

#### It's setup is as straight forward as it can get: 
* Create a repository 
* In the repository, install `testcafe` locally with the command `npm install testcafe --dev-save`. 
Now you can start going through the documentation [Here](https://devexpress.github.io/testcafe/documentation/getting-started/) and start on the tests.


## Postman

Once you're accustomed to the Web Platform and understand how HTTP communication works between the client and the server, you can simulate some API requests with Postman. Postman is an easy-to-use tool for **API testing**. You can download Postman [Here](https://www.getpostman.com/) and start having fun.


## FrisbyJS

If you're looking for an automated **REST API testing** replacement for Postman, we present you FrisbyJS. Frisby comes with an easy setup and an easy to understand syntax. Integrated with a testing platform like Jest or Jasmine, this is an excellent setup for API testing. You can find more information about how to use Frisby on the documentation [page](https://www.frisbyjs.com/installation.html) or on [Frisby Github](https://github.com/vlucas/frisby)


## Jmeter

Jmeter is a **performance testing** tool, which allows you to perform Load & Stress testing on your application. The tool setup is straigh-forward: you need to download it from [Here](http://jmeter.apache.org/download_jmeter.cgi) and on the command line, just run `jmeter` to open the GUI mode, but the test setup needs a little documentation, which can be found [Here](http://jmeter.apache.org/index.html). 


## Selenium & Cucumber ( optional )

If for some reason, Testcafe is not a satisfactory option for your **end-to-end testing**, there is always Selenium as back-up plan. Selenium supports tests in many languages and it can be easily integrated with [Cucumber](https://cucumber.io/docs), which is a very helpful tool for organizing the tests in a Given-When-Then format and making them understandable by all parties involved. Because this setup is less straight-forward than the previous examples, you can follow [this](https://docs.google.com/document/d/1GKDSiPltddffuthqKtgYuVcNiorrqKjzWfCZChA_FPs/edit) example on how to get started.

If you're not a fan of headaches, there's a [git repository](https://github.com/LaszloQ/WebdriverJSDemo) with the setup done, which you can just clone and test it out.


## Appium
So far we've covered browser e2e testing, api testing and performance testing, but we need a sollution for **mobile app testing** so here comes Appium in the picture. Appium can be intergrated with numerous other tools in order to get the testing setup of your need. For further documentation, you can check out [the official page](http://appium.io/).


> Good luck on your journey.
