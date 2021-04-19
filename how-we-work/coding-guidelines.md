## The art of clean code and consistency

Writing code is an essential part our day to day activity. While working together for several years now, we saw that adopting a single guideline for the entire team is very beneficial and powerful. Choosing between two or more ways of writing code can lead to a lot of [bikeshedding](https://en.wiktionary.org/wiki/bikeshedding).

### Styleguide

We follow most of the [airbnb styleguide](https://github.com/airbnb/javascript), which we highly recommend you read and understand before coming to an interview or sharing some code with us. We adapted some of the rules to enhance readability based on some debated preferences of the team members. You can read more about our reasoning on [Alex Moldovan's FreeCodeCamp account](https://medium.freecodecamp.org/adding-some-air-to-the-airbnb-style-guide-3df40e31c57a).

On our projects, we are using the following [ESLint config](https://github.com/FortechRomania/eslint-config-fortech) to make sure we all stick to the same guidelines. What's more, we make sure that code that does not pass the linter, does not end up in the central repository.

### Clean code

On top of a healthy coding styleguide comes the craftsmanship for writing clean and reusable code. We are 100% oriented towards quality and resilience when writing code. In our view, clean code equals less time spent over time refactoring and keeping the codebase up to date. We strongly encourage everyone that joins or wants to join the team to get familiar as soon as possible with the main principles behind clean code, many of which are addressed in Robert Martin's [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882).

Briefly, here are the principles:

1. Use very descriptive names. Be consistent with your names.

2. A function should not do more than one thing.

3. SRP (Single Responsibility Principle): a class or module should have one, and only one, reason to change.

4. Stepdown rule: every function should be followed by those at the next level of abstraction (low, intermediate, advanced).

5. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment.

6. The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification and then shouldn't be used anyway.

7. Flag arguments are ugly. Passing a boolean into a function is loudly proclaiming that this function does more than one thing. It does one thing if the flag is true and another one if the flag is false.

8. Write learning test when using third-party code to make sure it behaves the way you expect it to. And if codebase changes in time, at least you find out early enough.
