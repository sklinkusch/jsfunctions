# Regular Expressions (Regex, Regexp, RegEx, or RegExp)

Regular expressions are patterns used for character recognition in strings.

## Creation of a regular expression

There are two ways in creating a regular expression:

### Calling the constructor
```javascript
const re = new RegExp("ab+c");
```
In this case, the pattern is written as a string that is used as the argument of the `RegExp` constructor.

### Using the slash operator
```javascript
const re = /ab+c/
```
In this case, the pattern is enclosed in slashes. Note, that a slash within the pattern has to be escaped as `\/`.