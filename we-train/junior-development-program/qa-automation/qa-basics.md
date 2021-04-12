### Test cases

1. How to write a test case?
   Don't you know how to write test cases? No problem. Check out this [tutorial](https://www.guru99.com/test-case.html).
2. Sample test scenarios for testing web applications?
   Never seen a test scenario? Well.. [here](http://www.softwaretestinghelp.com/sample-test-cases-testing-web-desktop-applications/) are 180+ samples.
3. [Points to follow/writing hacks](https://www.qasymphony.com/blog/5-manual-test-case-writing-hacks/)

### Selectors

In order to performs actions on any page elements through an automation tool, first we need to identify the element with a selector so that the tool can recognize and interact with it. Automation tools support a variety of selectors, like:
* [IDs](https://www.w3schools.com/tags/att_global_id.asp)
* [ClassName](https://www.w3schools.com/html/html_classes.asp)
* [Xpath](https://www.w3schools.com/xml/xpath_intro.asp) & [Xpath Cheatsheet](https://devhints.io/xpath)
* [CSS Selectors](https://www.w3schools.com/cssref/css_selectors.asp)

Example: On a webpage, you want to click the "Dogs" button from the following html structure:
```[HTML]<div>
  <ul class="navbar">
    <li>
      <button> Cats </button>
    </li>
    <li>
      <button> Dogs </button>
    </li>
    <li>
      <button> Weasels </button>
    </li>
  </ul>
</div>
```
There are several ways to "catch" the button, this is only one example of how to do this:
* Using css selectors: `.navbar > li:nth-of-type(2) > button`
* Using xpath: `//ul[@class='navbar']/li[2]/button`
