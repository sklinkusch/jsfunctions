# Regular Expressions (Regex, Regexp, RegEx, or RegExp)
Regular expressions are patterns used for character recognition in strings. They consist of simple characters and special characters.
Regular expressions originate in the script language Perl.

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

### Special characters
There are several characters that have a special meaning when using regular expressions. They are put into a number of groups according to
their purposes:

- Character classes, such as numbers, alphabetical characters, whitespaces
- Assertions, e.g. beginning and end of a line or word
- Groups
- Backreferences (not covered here)
- Quantifiers

**Note:** If the real character is meant within a regular expression, it must be escaped with a backslash before it.

#### Character classes
There are some general character classes. The most important ones are mentioned in the following list:

- `[a-c]` or `[wxz]`: This is a general character class. It is matched for any of the characters given in the class.
- `[^a-c]` or `[^wxz]`: This is a negated character class. It is matched for any character except the ones given in the class.
- `.`: This is any single character.
- `\d` or `[0-9]`: This is any digit (Arabic numeral).
- `\D` or `[^0-9]`: This is any character but no digit (Arabic numeral).
- `\w`: This is an alphanumeric character or the underscore, i.e. the same as `[A-Za-z0-9_]`.
- `\W`: This is any character that is not alphanumeric or the underscore, i.e. the same as `[^A-Za-z0-9_]`.
- `\s`: This is a single whitespace character, e.g. a space, a tab, a form feed, or a line feed.
- `\S`: This is any character that is not a whitespace.
- `\t`: This is a horizontal tab.
- `|`: This is a disjunction. It shows two alternatives. The expression `/creator|player/` is matching for `"creator"` as well as for
  `"player"`.

#### Assertions
Assertions are special characters used to mark boundaries or conditions.

- `^` (not within character classes): This shows the beginning of a line or document.
- `$`: This shows the end of a line or document.
- `\b` (not within character classes): This shows the beginning or end of a word.
- `\B`: This shows a non-word boundary.
- `x(?=y)`: This is a lookahead assertion. It matches `x` only when it is followed by `y`. The `y` is not part of the match results.
- `x(?!y)`: This is the negative lookahead assertion. It matches every `x` that is not followed by `y`.
- `(?<=y)x`: This is a lookbehind assertion. It matches `x` only it follows `y`. The `y` is not part of the match results.
- `(?<!y)x`: This is the negative lookbehind assertion. It matches every `x` that does not follow `y`.

#### Groups
Patterns can be grouped into groups.

- `(x)`: This is a group. The group is then remembered and accessible from the RegExp object's properties.
- `(?<Name>x)`: This is a named captured group. Here, `x` is captured and stored under the name `Name`.
- `(?:x)`: Non-capturing group. Every group that is not used later should be made like this for performance issues.

#### Quantifiers
Quantifiers tell us how often a character, a character class, or a group should occur in a string.

- `x*`: The asterisk stands for at least zero consecutive occurrences of `x`.
- `x+`: The plus sign stands for at least one consecutive occurrence of `x`.
- `x?`: The question mark stands for zero or one occurrence of `x`.
- `x{n}`: A non-negative whole number `n` in curly braces stands for exactly `n` consecutive occurrences of `x`.
- `x{n,}`: A non-negative whole number `n` followed by a comma in curly braces stands for `n` or more consecutive occurrences of `x`.
- `x{n,m}`: Two non-negative whole numbers `n` and `m` (`m>n`) in curly braces, separated by a comma, stand for `n` to `m` consecutive
  occurrences of `x`.
- A question mark after a quantifier makes the regular expression "non-greedy", i.e. they stop searching if the condition is fulfilled. This
  can be described with an example:

```javascript
const string = '<div><p><span>Hi!</span></p></div>';
const greedyRegExp = /<.*>/;
const nonGreedyRegExp = /<.*?>/;
```
If we test the string with the two regular expressions, they will return a different number of occurrences. The first one will return one
occurrence (the whole string), while the second one will return six occurrences (`"<div>"`, `"<p>"`, `"<span>"`, `"</span>"`, `"</p>"`, and
`"</div>"`).

### Flags
Regular expressions may have flags that can enhance the functionality when searching with the pattern.

| flag | description | property |
|------|-------------|----------|
| `d`  | generate indices for substring matches | `hasIndices` |
| `g`  | general search | `global` |
| `i`  | case-insensitive search | `ignoreCase` |
| `m`  | allows `^` and `$` to match newline characters | `multiline` |
| `s`  | allows `.` to match newline characters | `dotAll` |
| `u`  | treat a pattern as a sequence of Unicode code points | `unicode` |
| `v`  | upgrade to the `u` mode with more unicode feature | `unicodeSets` |
| `y`  | sticky search, matches starting at the current position | `sticky` |