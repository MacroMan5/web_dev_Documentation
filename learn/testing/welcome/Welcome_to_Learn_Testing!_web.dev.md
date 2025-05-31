# Welcome to Learn Testing!  |  web.dev

**Source URL:** [https://web.dev/learn/testing/welcome?continue=https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%23article-https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%2Fwelcome](https://web.dev/learn/testing/welcome?continue=https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%23article-https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%2Fwelcome)  
**Last Updated:** 2025-05-23T01:01:12.039Z  
**Extracted:** 2025-05-31 16:58:10

---

# Welcome to Learn Testing! | web.dev

This course is an introduction to and exploration of testing for the web.

In this course, you'll learn about the following:

*   Testing fundamentals
*   Automated versus manual testing
*   Where and how to run your tests
*   Best practices
*   The philosophy of testing, including what to test, who's responsible, and how to consider testing a means to an end, not as an objective itself.

The course also includes concise, practical sample code to learn from.

The course's scope includes JavaScript and the document model on frontend as well as library testing on the backend, run in an environment like Node.js. It assumes no background in testing, but you'll need a grounding in JavaScript and experience with Node.js or similar. It's suitable for both novice and experienced developers.

Because most testing frameworks and tools share a common language, Learn Testing takes a general approach to testing. Where it's important to get specific, we'll use [Vitest](https://vitest.dev/), a test framework that's growing in popularity, and demonstrate how to test components for the web written using [React](https://react.dev/) or [Lit](https://lit.dev/). To learn more about this choice, see the [appendix](https://web.dev/learn/testing/appendix).

You can go through this course from beginning to end, but you can also use it as a reference for specific topics. Where relevant, the course links to resources.

Here's what you'll learn:

## Get started with testing

### [What testing is](https://web.dev/learn/testing/get-started/what-testing-is)

This is a high-level introduction to testing, including practical examples of testing in JavaScript. It also includes an introduction to the scale of each test.

### [Where tests run](https://web.dev/learn/testing/get-started/where-tests-run)

Tests can help you be productive and write software efficiently, and while it's possible to run them manually using a command line, you can also run them as part of an automated process or build system.

### [The testing environment](https://web.dev/learn/testing/get-started/testing-environment)

Runtime tools like Node are for general-purpose code, and testing code for the browser can either be run in an emulated environment or using a framework designed for browser testing.

### [Types of automated testing](https://web.dev/learn/testing/get-started/test-types)

Learn about common categorizations of test types, which mostly correspond to their scale. Importantly, test types don't have a strict definition and will change based on your needs.

### [What to test and your approach](https://web.dev/learn/testing/get-started/what-to-test)

Identifying the most important parts of your codebase to apply rigorous testing to can be a tough decision. This module introduces the idea of testing as a means to an end, and how to assess your code for testing.

### [Component testing in practice](https://web.dev/learn/testing/get-started/component-testing)

In this practical module, you'll learn how to test a not-so-ideal React component. This uses Vitest through three distinct examples: intercepting network traffic made with `fetch()`, mocking an external dependency, and using React's `Context` to provide a custom bit of code just for the test.

### [Static analysis](https://web.dev/learn/testing/get-started/static-analysis)

Using tools like TypeScript and ESLint, while not well-established approaches to testing, can provide a type of automated checking. This module discusses these alternative tools.

## Assertions and other primitives

### [Tools of the trade](https://web.dev/learn/testing/assertions/tools)

Learn about the primitives common to most testing libraries or frameworks, including `test()` and `assert`, that will be mainstays of every test you write in JavaScript.

### Coming soon

*   Avoid common test pitfalls
*   Test doubles
*   Test libraries and utilities
*   Decide on a test framework

The remainder of this section will contain more pages on test frameworks and libraries, the way they should be used, and how to decide on which one and what other tools to use.

## Coming soon: Problem-driven testing

You'll learn patterns to approach a number of common Web testing challenges.

## Coming soon: Automated testing in practice

This is a practical section showing how to test an ecommerce site built with Next.js, including code you can check out and learn yourself. You'll learn how to test its components, how to work with its external services, including payment, for testing, and how to build end-to-end tests for a site that has an optional login page.

## Coming soon: The philosophy of testing

Testing can be an engineering challenge, but knowing what to test, who's responsible, and best practices can also be a challenge for a development team.

## Coming soon: Writing testable code

This course provides guidance on testing code _as it exists_, but your team can adopt various patterns to make your code easier to test. This section will cover some approaches.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
