# QA Internship Roadmap


## Introduction and Setup
1. Setup Github account.
  For guidance check out this [link](https://help.github.com/articles/set-up-git/).
  Learn [Git essentials](https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html)
  Set up a Git repository for Automation testing
2. Setup editor of choice.
  We recommend one on the following:
    * [Virtual Studio Code](https://code.visualstudio.com/)
    * [Atom](https://atom.io/)
  Add plugins like [ESLint](https://eslint.org/) or [Emmet](https://emmet.io/) to your editor.
  For Atom, install the following packages:  atom-beautify, atom-ternjs, cucumber

## The Web Platform
1. Understand [how the internet works](https://ed.ted.com/on/tdUFCocK)
2. Understand how a browser works.
  At this [link](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/) you can find an interesting tutorial that includes general functioning of a browser, its structure, rendering engines and HTML or CSS code parsing.
3. Learn a little about HTTP and HTTPS. Understand the following:
    * [Requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
    * [Responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
    * [Methods](https://www.tutorialspoint.com/http/http_methods.htm)
    * [Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
4. What is CRUD and what is a [RESTful API](http://www.restapitutorial.com/lessons/httpmethods.html)?
  Practice API skills on the [tutorial](https://www.lynda.com/Flask-tutorials/CRUD-REST-basics/521200/533063-4.html)
  Install [Postman](https://www.getpostman.com/postman) and play around with the tool.
6. What is a [cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)?
7. What is a [session](https://developer.mozilla.org/en-US/docs/Web/HTTP/Session)?


## Introduction to programming
    + HTML & CSS
      Learn about elements, selectors and attributes by practicing on this [tutorial](https://www.lynda.com/HTML-tutorials/HTML-Essential-Training/170427-2.html).
    + Javascript
      1. Learn about Data Structures.
      There is an interesting book that discusses about data structures and algorithms. You can find it [here](https://github.com/wikisoft/collection)
      2. Get familiar with JavaScript
        * [Basics](https://app.pluralsight.com/paths/skills/javascript)
        * [Function Definitions](http://eloquentjavascript.net/03_functions.html)


## QA basics
### Test cases
1. How to write a test case?
  You don't know how to write test cases? No problem. Check out this [tutorial](https://www.guru99.com/test-case.html).
2. Sample test scenarios for testing web applications?
  Never seen a test scenario? Well.. [here](http://www.softwaretestinghelp.com/sample-test-cases-testing-web-desktop-applications/) are 180+ samples.
3. [Points to follow/writing hacks](https://www.qasymphony.com/blog/5-manual-test-case-writing-hacks/)

### Selectors
1. Learn Xpath expressions
2. Create variables for elements using:
  + [Xpath](https://www.w3schools.com/xml/xpath_intro.asp)
  + [ClassName](https://www.w3schools.com/html/html_classes.asp)
  + [IDs](https://www.w3schools.com/tags/att_global_id.asp)
  + [CSS Selectors](https://www.w3schools.com/cssref/css_selectors.asp)


## Testing Tools
### Testcafe
  1. Install [Testcafe](https://devexpress.github.io/testcafe/)

### Selenium Webdriver
  1. Install Selenium Webdriver.
  2. Install browser drivers
  3. Install [Cucumber](https://github.com/cucumber/cucumber-js)
  4. Install [Chai](http://chaijs.com/)

## Automation test scenario creation
1. Create test scenarios based on the test cases & QA Checklist, using Cucumber / Testcafe
2. Create the test step definitions
