# Javascript functions

This is a collection of useful Javascript functions for different types.

## Table of Contents
1. [Array functions](#array)
   1. [Loop-based functions](#array-loop)
      1. [Array.forEach](#forEach)
      1. [Array.map](#map)
      1. [Array.filter](#filter)
      1. [Array.find](#find)
      1. [Array.findLast](#findlast)
      1. [Array.findIndex](#findindex)
      1. [Array.findLastIndex](#findlastindex)
      1. [Array.reduce](#reduce)
      1. [Array.sort](#sort)
          1. [sort by ASCII characters](#sortascii)
          1. [numerical sorting](#sortnumbers)
          1. [alphabetical sorting](#sortalphabetical)
          1. [sorting with locales](#sortlocales)
      1. [Array.some](#some)
      1. [Array.every](#every)
   1. [Non-loop-based functions](#array-nonloop)
      1. [Array.concat](#concat)
      1. [Array.fill](#fill)
      1. [Array.flat](#flat)

## Array functions<a name="array"></a>

### Loop-based functions<a name="array-loop"></a>

In the following functions, the parameters `index` and `array` are optional.
They should be only used if these values are necessary within the callback function.

#### `Array.forEach`<a name="forEach"></a>
```javascript
Array.forEach((item, index, array) => {
  // do some stuff
});
```
This function is just a replacement for a `while` or `for` loop. Inside the
callback, there is no return statement.

#### `Array.map`<a name="map"></a>
```javascript
const newArray = Array.map((item, index, array) => {
  // do some stuff
  return anything;
});
```
This function takes the array and returns an array of equal size. A return
statement in the callback function is required. These return values are the
elements of the new array.

#### `Array.filter`<a name="filter"></a>
```javascript
const newArray = Array.filter((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
});
```
This function takes the array and returns an array with all elements whose
elements match the condition given in the callback function. Thus, a boolean has
to be returned inside the callback function.

#### `Array.find`<a name="find"></a>
```javascript
const firstMatchingItem = Array.find((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
});
```
This function takes the array and returns the first element that matches the
condition given in the callback function. Thus, a boolean has to be returned
inside the callback function.

#### `Array.findLast`<a name="findlast"></a>
This function does the same as [`Array.find`](#find) but iterates the array from
the last to the first item. Thus, the last matching item is found and returned.

#### `Array.findIndex`<a name="findindex"></a>
```javascript
const indexOfFirstMatchingItem = Array.find((item, index, array) => {
  // do some stuff
  return boolean; // true or false
});
```
This function takes the array and returns the index of the first element that
matches the condition given in the callback function. Thus, a boolean has to be
returned inside the callback function.

#### `Array.findLastIndex`<a name="findlastindex"></a>
This function does the same as [`Array.findIndex`](#findindex) but iterates the
array from the last to the first item. Thus, the index of the last matching item
is found and returned.

#### `Array.reduce`<a name="reduce"></a>
```javascript
const singleValue = Array.reduce((accumulator, item, index, array) => {
  // do some stuff
  return valueForLoopTurn;
}, startValue);
```
This function takes the array and returns a single value. This value can be of
any type (string, number, boolean, array, object, ...). The start value (usually
`0`, `''`, `[]`, `{}`, `true`, `false`) is the accumulator in the first turn.
The return value in the callback function in one loop turn is the accumulator in
the next turn. The return value in the last loop turn is the return value of the
whole function. This way, one can sum up the values of an array, compose a
string or sequentially build up an array or object.

#### `Array.sort`<a name="sort"></a>
```javascript
const sortedArray = Array.sort((a, b) => {
  // do stuff
  return number;
});
```
This function takes the array and sorts it according to the callback function.
The two parameters `a` and `b` are two elements of the array that are compared
to each other. The return value is always a number that can be negative, `0`, or
positive. For a positive value, the order of the two elements is reversed,
otherwise not. 

##### sort by ASCII characters<a name="sortascii"></a>
The easiest way to sort is by ASCII characters. This means, the first characters
are compared to each other, then the second characters, and so on. The case of
the characters matters, so `A` and `a` are different characters. In this case,
the sorting function can be omitted, thus:
```javascript
const sortedArrayByAscii = Array.sort();
```

##### sort by numbers<a name="sortnumbers"></a>
Another easy way to sort is a numeric sorting. This can be achieved by returning
the difference between `a` and `b`.
```javascript
const sortedArrayNumerical = Array.sort((a, b) => a - b);
```

##### sort alphabetically (without locales)<a name="sortalphabetical"></a>
In this case, everything has to be transformed either to upper or to lower case.
After this, a sort by ASCII characters is possible.
```javascript
const sortedArrayAlphabetical = Array.sort((a, b) => {
  const nameA = a.toLowerCase();
  const nameB = b.toLowerCase();
  return nameA < nameB ? -1 : nameA > nameB ? +1 : 0;
});
```

##### sort alphabetically (with locales)<a name="sortlocales"></a>
If certain words from a language different from English have to be sorted,
special settings have to be made. These languages may contain special
characters and a special sorting of characters.
```javascript
const sortedArrayLocale = Array.sort((a, b) => {
  const nameA = a.toLowerCase();
  const nameB = b.toLowerCase();
  return nameA.toLocaleCompare(nameB, language, options);
});
```
with the following languages:

| abbr. | language     |
|----|-----------------|
| ar | Arabic          |
| nl | Dutch           |
| en | English         |
| es | Spanish         |
| fr | French          |
| de | German          |
| it | Italian         |
| pl | Polish          |
| pt | Portuguese      |

and the other options (options are given as an object):
* **numeric** *(boolean)*: when set to `true`, numeric strings are compared as
  numbers, default is `false`
* **caseFirst** *(string)*: whether upper (`"upper"`) or lower (`"lower"`) case
  letters should be sorted first, default is `"false"` (no priority between
  upper and lower case letters)
* **sensitivity**: *(string)*: difference between letters with or without
  diacritical symbols and cases. Possible values are (default: `"variant"`):
  * **`"base"`**: only strings that differ in base letters are unequal, e.g.
    `"a" ≠ "b"`, `"a" = "à"`, `"a" = "A"`
  * **`"accent"`**: like `"base"`, but also accented letters are unequal to the
    respective unaccented letters, e.g. `"a" ≠ "b"`, `"a" ≠ "à"`, `"a" = "A"`
  * **`"case"`**: like `"base"`, but also letters that differ in case are unequal,
    e.g. `"a" ≠ "b"`, `"a" = "à"`, `"a" ≠ "A"`
  * **`"variant"`**: like `"accent"`, but also letters that differ in case are
    unequal, e.g. `"a" ≠ "b"`, `"a" ≠ "à"`, `"a" ≠ "A"`
* **ignorePunctuation** *(boolean)*: whether punctuation should be ignored,
  default is `false`.

#### `Array.some`<a name="some"></a>
```javascript
const doesOneElementFit = Array.some((item, index, array) => {
  // do some stuff
  return boolean; // true or false
});
```
This function checks if at least one element of the array matches the condition
given in the callback function. This callback function must return a boolean,
dependent on if the condition is matched.

#### `Array.every`<a name="every"></a>
```javascript
const doAllElementsFit = Array.every((item, index, array) => {
  // do some stuff
  return boolean; // true or false
});
```
This function checks if all elements of an array match the condition given in
the callback function. This callback function must return a boolean, depending
on if the condition is matched.

### Non-loop-based functions<a name="array-nonloop"></a>

#### `Array.concat`<a name="concat"></a>
```javascript
const mergedArray = array1.concat(array2);
```
This function merges two arrays by appending the elements of the second array to
the first array. It does the same as `[ ...array1, ...array2 ]`.

#### `Array.fill`<a name="fill"></a>
```javascript
const filledArray = Array.fill(replaceValue, start, end);
```
This function replaces the elements from the index `start` to `end - 1` within
the source array with `replaceValue`. The parameters `start` and `end` are
optional. If `end` is omitted, all elements from the `start` to `Array.length - 1`
are replaced. If `start` and `end` are omitted, all elements of the source array
are replaced.

#### `Array.flat`<a name="flat"></a>
```javascript
const flatArray = Array.flat(flatDegree);
```
This function takes an array containing also sub-arrays and creates a new array
where the sub-arrays are concatenated up to a depth of `flatDegree`. This
parameter is optional. If it is omitted, it is set to `1`. The parameter
`flatDegree` is a positive number or `Infinity`. In the latter case, all
sub-arrays are concatenated, resulting an array containing all elements in the
array and sub-arrays.