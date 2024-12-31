# Naming Things in Programming

# Avoid (most) Abbreviations

Specifically only use pronounceable names abbreviations like “props” or “org”, but don’t use “tmp” or “src” - your job is a software engineer is to communicate as clearly as possible the solution to the requirements. When it comes to programming, that “clarity “is about implementing a correct solution from end to end across all possible input. When it comes to communicating in your code to the next developer who might be looking at it, which might be used on the line, it is good English and minimum assumptions about what the reader understands. ￼

NEVER USE:

- "tmp"
- "src"

# Extreme Consistency!

### Acronyms are treated as words!

The industry is a mess with inconsistency about how to capitalize acronyms. It MUST be done consistently and MUST be done in a way that they can be automatically converted between various code-word encodings. The ONLY answer I can see is they must be treated just like any other word:

- MyHtml, UserId, DynamoDb
- myHtml, userId, dynamoDb
- my-html, user-id, dynamo-db
- MY_HTML, USER_ID, DYNAMO_DB

```javascript
// given this
a = toLowerCase(varName);

// all these MUST be true - i.e. they must be no-ops
assert.equal(a, toLowerCase(toDashCase(a)));
assert.equal(a, toLowerCase(toUpperCamelCase(a)));
assert.equal(a, toLowerCase(toSnakeCase(a)));
```

Bad examples:

- `ID` all caps is an anti-pattern. `toDashCase("userID") === "user-id"` and `toLowerCamelCase("user-id") === "userId"` and `"userId" !== "userID"` FAIL

### Don’t run together words

`normaladdr` should be `normalAddr` - personally, I’d prefer `addressNormalizer`

### Don’t be afraid of long names!

Code-completion makes them “free” and readability really benefits!

What does `normalAddr` do??? What does `addressNormalizer` do?

# Don’t Use Hungarian Notation!

### Objections:

1. My main objection is types of variables should be allowed to change without needing to change their names!
2. It gets you _nothing_ you can’t get elsewhere. It’s mostly used in typed languages, so the type of the variable is already known. Any modern editor will tell you the type if you hover over it. It just creates noise.
3. It’s not minimal. I.e. It decreases the information density of your code. Damn, I really need a name for my principle of minimizing code-size: as long as it doesn’t (seriously) impact readability, less-code is better code. i.e. maximize information density of your code
4. It breaks consistency: Perhaps the worst problem is it fails completely if you need to represent a given type in different encodings:
   > Here’s a real-world example I ran into: An ID was expressed as a double-word (64 bits). So it was called itemDwId in one context. Then it got exported as JSON. JSON can’t represent double-words, so it must be represented as a string. Now you’re damned either way:
   >
   > - If you stay consistent, you name it itemDwId - and that’s just factually wrong. It’s a string, not a double-word.
   > - OR you break consistency and change the name to itemStringId in which case you can no longer search your code for all uses of itemDwId.
   >   Just use `itemId` for the love of god!

Really, names, both variable and function, should encode the _semantics_ of that variable - what is the _meaning_ of it - not the syntax, encoding or other “SOAP” artifacts of the code.

# Example JavaScript Naming Conventions

Folder and file names are considered code just like their contents. For consistency, we name folders and files follow the same naming conventions as JavaScript:

1. `UpperCamelCase` for Classes, Types and Modules.
2. `lowerCamelCase` for variables and functions.

Folders will always be UpperCamelCase as they are considered Modules.

Files will be named for their primary export. If they have a default export, the file name should be identical to the export name. In general, though, we avoid default exports. It tends to be less flexible under refactoring.

# Naming Patterns

## File & Directory Names

- should match their primary export (or if they have a default export, they MUST match that export)
- And I mean -exactly- match the primary export.

> _File and Directory names are part of the source code._

## Functions

- should be verbs or verb phrases

## OO Naming (classes)

- methods should named like functions
  - typically, the variable holding the object will be considered the noun:
  - `user.submit()` - submit is the verb, user is the noun
- getters: getters should be nouns
  - use getters as getters, not functions as getters:
  - `user.name` would use the bar getter
  - `user.name()` is an anti-pattern
    - it leaves the reader wondering, does this mutate something? does this return a cloned object with a new value?
    - In this case in particular, “name” is both a noun and a verb. Maybe this is a setter: `user.name("frank")` - name the user.
    - use a getter if your language supports it (JavaScript, C++ and Ruby all do - most OO does)
  - if you need to have parameters for your getter, use the `get` verb: `this.getName(format: enum)`
  - This pairs will with just `this.name` for the option-less, common version.
  - This helps minimize code size and clarity.
  - All read-only operations are either a getter or start with `get`
- Exception: Declarative DSLs
  - it may make sense to have method names without verbs in them if you are designing a DSL using OO. I still advocate for using getters wherever possible, but if you want a `this.description("...")` to declare the description of something, that can be OK. Just restrict this pattern to classes that are explicitly using the declarative-DSL pattern.
  - i.e. all the function names should be delarative and all the functions that declare something either mutate or return a new instance of the object with the declaration applied (pure-functional)
  - get-methods should still follow the rule: either use a getter or use the `getFoo` naming convention
  - Ruby: bonus points for Ruby, it lets you have a getter AND a separate function that gets triggered whe you invoke it. In that way you can have both a getter and declararer with same signature: `user.name` to get the name, `user.name(“george")` to set the name. Ruby also lets you have the 3rd option of a setter - `user.name = "george"` which invokes your setter function.

# Placeholder Names (lib, utils, temp)

## "Lib" vs "Util"

For young modules, it's useful to have placeholder names until their purpose is clear. Settle on a standard! Don't use both `lib` and `utils` for the young modules. I like "lib", but consistency is what matters. Make a good guess what the module is about and append "lib": e.g. `userLib`, 'stringLib', 'dateLib', etc.

## "Temp"

Just don't use it. Obviously they are a code-smell, but they suggest a few specific problems:

- Many temp variables are single-use. We've already established that single-use variables increase code-size and are therefor counterproductive. Just inline the code where it is used. If it feels complex, make a helper function instead.
- It's OK to use common, better named variables like
  - standard iteration variables like 'i', 'j', 'k', etc. Why is this OK? Because their purpose is very clear due to their standard usage.
  - Also, "v" and "k" for value and key when iterating over an object or map serve a similar purpose.
- In general, "temp" variables suggest there may be a better way to organize the code.
