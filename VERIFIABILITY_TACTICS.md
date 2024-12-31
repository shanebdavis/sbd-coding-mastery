# Modular Testing - Test from the Outside

It's simple:

> Always test from the outside.n

> NOT: ~~unit, integration, or end-to-end~~ testing

## Isolate tests from code

1. Put all tests in their own directory under source: /source/tests
2. /source/tests should be organized in a folder structure that parallels the source code.

Why?

- We are trying to minimize code-size. If tests are mixed with source code, it makes it harder to minimize the surface area of the next change. Your search tools will search in code AND tests. Your directory listings will have extra files (tests) in them. In general, when problem-solving you want to ONLY look at the code, not the tests.
- Putting tests separate also supports modular design and modular testing. It emphasizes that we want to TEST FROM THE OUTSIDE. When it's time to factor out a module into it's own package, it's easy to move the matching tests with it. (Admittedly, it's even easier when test are inline with the code, but the cost is too high.)
- We want to monitor how big our overall code is AND how big our overall tests are. If they are separate, it's easy to measure both.

Caveats:

- This does mean tests will break the rule of "never import the sub-files and sub-folders of any other folder". This is allowed because Organic Modular Design means modulization is always in flux. We are always increasing modularity, we aren't striving for perfect modularity. Further,

# Pure Functions are your Friends

- Separate functional logic from integrations for easier testing and modular design.
- Apply this principle to testing user interfaces by isolating logic from direct interactions.
