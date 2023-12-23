# Regular Expressions (Regex, Regexp, RegEx, or RegExp)
Regular expressions are patterns used for character recognition in strings. They consist of simple characters and special characters.

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

## Writing a regular expression
### Simple expressions
A simple expression consists only of alphanumeric characters. An example for such a simple regular expression would be:

```javascript
const simpleRegExp = /holidays/;
```
This regular expression searches a text for all occurrences of **holidays** (in small letters). Usually, for such a simple task, a regular
expression is not necessary.