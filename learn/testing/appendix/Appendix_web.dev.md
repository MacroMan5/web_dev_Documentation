# Appendix  |  web.dev

**Source URL:** [https://web.dev/learn/testing/appendix?continue=https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%23article-https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%2Fappendix](https://web.dev/learn/testing/appendix?continue=https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%23article-https%3A%2F%2Fweb.dev%2Flearn%2Ftesting%2Fappendix)  
**Last Updated:** 2025-05-23T01:01:43.863Z  
**Extracted:** 2025-05-31 16:58:10

---

# Appendix  |  web.dev

Appendix

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Here are some additional concepts and information that may help on your test development journey.

## Vitest as a test runner

[Vitest](https://vitest.dev/) is a test runner and framework that's growing in popularity. This course uses it whenever specific examples are required, but many of the samples included are generic and apply to whatever framework you've chosen.

Most runners or test frameworks tend to have a lot in common, and this course will be useful regardless of your chosen stack. We've chosen to focus on Vitest for a number of reasons:

*   It's modern and involves very little work to set up or configure, as opposed to other test runners. While it's built on the [Vite](https://vitejs.dev/) build tool, Vitest still works with existing projects.
    
*   It also has great support for working with [EcmaScript Modules (ESM)](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/), including mocking whole imports. While it has [some caveats](https://vitest.dev/api/vi.html#vi-mock), it's more stable than other tooling.
    

Most importantly, it presents a largely compatible API to Jest, likely the most [popular](https://npm-stat.com/charts.html?package=jest&package=vitest&from=2017-11-15&to=2023-11-15) runner. But again, the way you structure and group your tests tends to be similar no matter which framework you're using. More advanced features, like complicated test doubles, tend to stray a bit further. This course uses Vitest to describe them, but always describes the generic solution as well.

## React as a component model

While this course does provide general code examples that test plain JavaScript, for example, mathematical functions, it rapidly moves into testing React components before later including Web Components generally and using Lit. This course also uses Next.js.

This is a practical choice. Despite criticisms, React is the most used framework of the participants in the [State of JS survey](https://2023.stateofjs.com/en-US/libraries/front-end-frameworks/).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
