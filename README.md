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
      1. [Array.from](#from)
      1. [Array.includes](#includes)
      1. [Array.indexOf](#indexof)
      1. [Array.isArray](#isarray)
      1. [Array.join](#join)
      1. [Array.lastIndexOf](#lastindexof)
      1. [Array.of](#of)
      1. [Array.pop](#pop)
      1. [Array.push](#push)
      1. [Array.reverse](#reverse)
      1. [Array.shift](#shift)
      1. [Array.slice](#slice)
      1. [Array.splice](#splice)
      1. [Array.unshift](#unshift)
      1. [Array.with](#with)

## Array functions<a name="array"></a>

### Loop-based functions<a name="array-loop"></a>

In the following functions, the callback parameters `index` and `array` are optional, as well as the general parameter `thisArg`. The latter
one tells the callback function which parameter to use as `this` within the callback. They should be only used if these values are necessary
within the callback function.

#### `Array.forEach`<a name="forEach"></a>
```javascript
sourceArray.forEach((item, index, array) => {
  // do some stuff
}, thisArg);
```
This function is just a replacement for a `while` or `for` loop. Inside the callback, there is no return statement.

#### `Array.map`<a name="map"></a>
```javascript
const newArray = sourceArray.map((item, index, array) => {
  // do some stuff
  return anything;
}, thisArg);
```
This function takes the array and returns an array of equal size. A return statement in the callback function is required. These return
values are the elements of the new array.

#### `Array.filter`<a name="filter"></a>
```javascript
const filteredArray = sourceArray.filter((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
}, thisArg);
```
This function takes the array and returns an array with all elements whose elements match the condition given in the callback function.
Thus, a boolean has to be returned inside the callback function.

#### `Array.find`<a name="find"></a>
```javascript
const firstMatchingItem = sourceArray.find((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
}, thisArg);
```
This function takes the array and returns the first element that matches the condition given in the callback function. Thus, a boolean has
to be returned inside the callback function.

#### `Array.findLast`<a name="findlast"></a>
This function does the same as [`Array.find`](#find) but iterates the array from the last to the first item. Thus, the last matching item is
found and returned.

#### `Array.findIndex`<a name="findindex"></a>
```javascript
const indexOfFirstMatchingItem = sourceArray.findIndex((item, index, array) => {
  // do some stuff
  return boolean; // true or false
}, thisArg);
```
This function takes the array and returns the index of the first element that matches the condition given in the callback function. Thus, a
boolean has to be returned inside the callback function.

#### `Array.findLastIndex`<a name="findlastindex"></a>
This function does the same as [`Array.findIndex`](#findindex) but iterates the array from the last to the first item. Thus, the index of
the last matching item is found and returned.

#### `Array.reduce`<a name="reduce"></a>
```javascript
const singleValue = sourceArray.reduce((accumulator, item, index, array) => {
  // do some stuff
  return valueForLoopTurn;
}, startValue);
```
This function takes the array and returns a single value. This value can be of any type (string, number, boolean, array, object, ...). The
start value (usually `0`, `''`, `[]`, `{}`, `true`, `false`) is the accumulator in the first turn. The return value in the callback function
in one loop turn is the accumulator in the next turn. The return value in the last loop turn is the return value of the whole function. This
way, one can sum up the values of an array, compose a string or sequentially build up an array or object.

#### `Array.sort`<a name="sort"></a>
```javascript
const sortedArray = unsortedArray.sort((a, b) => {
  // do stuff
  return number;
});
```
This function takes the array and sorts it according to the callback function. The two parameters `a` and `b` are two elements of the array
that are compared to each other. The return value is always a number that can be negative, `0`, or positive. For a positive value, the order
of the two elements is reversed, otherwise not. 

##### sort by ASCII characters<a name="sortascii"></a>
The easiest way to sort is by ASCII characters. This means, the first characters are compared to each other, then the second characters, and
so on. The case of the characters matters, so `A` and `a` are different characters. In this case, the sorting function can be omitted, thus:
```javascript
const sortedArrayByAscii = unsortedArray.sort();
```

##### sort by numbers<a name="sortnumbers"></a>
Another easy way to sort is a numeric sorting. This can be achieved by returning the difference between `a` and `b`.
```javascript
const sortedArrayNumerical = unsortedArray.sort((a, b) => a - b);
```

##### sort alphabetically (without locales)<a name="sortalphabetical"></a>
In this case, everything has to be transformed either to upper or to lower case. After this, a sort by ASCII characters is possible.
```javascript
const sortedArrayAlphabetical = unsortedArray.sort((a, b) => {
  const nameA = a.toLowerCase();
  const nameB = b.toLowerCase();
  return nameA < nameB ? -1 : nameA > nameB ? +1 : 0;
});
```

##### sort alphabetically (with locales)<a name="sortlocales"></a>
If certain words from a language different from English have to be sorted, special settings have to be made. These languages may contain
special characters and a special sorting of characters.
```javascript
const sortedArrayLocale = unsortedArray.sort((a, b) => {
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
- **numeric** *(boolean)*: when set to `true`, numeric strings are compared as numbers, default is `false`
- **caseFirst** *(string)*: whether upper (`"upper"`) or lower (`"lower"`) case letters should be sorted first, default is `"false"` (no
  priority between upper and lower case letters)
- **sensitivity**: *(string)*: difference between letters with or without diacritical symbols and cases. Possible values are (default:
  `"variant"`):
  - **`"base"`**: only strings that differ in base letters are unequal, e.g. `"a" ≠ "b"`, `"a" = "à"`, `"a" = "A"`
  - **`"accent"`**: like `"base"`, but also accented letters are unequal to the respective unaccented letters, e.g. `"a" ≠ "b"`, `"a" ≠
    "à"`, `"a" = "A"`
  - **`"case"`**: like `"base"`, but also letters that differ in case are unequal, e.g. `"a" ≠ "b"`, `"a" = "à"`, `"a" ≠ "A"`
  - **`"variant"`**: like `"accent"`, but also letters that differ in case are unequal, e.g. `"a" ≠ "b"`, `"a" ≠ "à"`, `"a" ≠ "A"`
- **ignorePunctuation** *(boolean)*: whether punctuation should be ignored, default is `false`.

#### `Array.some`<a name="some"></a>
```javascript
const doesOneElementFit = sourceArray.some((item, index, array) => {
  // do some stuff
  return boolean; // true or false
}, thisArg);
```
This function checks if at least one element of the array matches the condition given in the callback function. This callback function must
return a boolean, dependent on if the condition is matched.

#### `Array.every`<a name="every"></a>
```javascript
const doAllElementsFit = sourceArray.every((item, index, array) => {
  // do some stuff
  return boolean; // true or false
}, thisArg);
```
This function checks if all elements of an array match the condition given in the callback function. This callback function must return a
boolean, depending on if the condition is matched.

### Non-loop-based functions<a name="array-nonloop"></a>

#### `Array.concat`<a name="concat"></a>
```javascript
const mergedArray = array1.concat(array2);
```
This function merges two arrays by appending the elements of the second array to the first array. It does the same as `[ ...array1,
...array2 ]`.

#### `Array.fill`<a name="fill"></a>
```javascript
const filledArray = sourceArray.fill(replaceValue, start, end);
```
This function replaces the elements from the index `start` to `end - 1` within the source array with `replaceValue`. The parameters `start`
and `end` are optional. If `end` is omitted, all elements from the `start` to `Array.length - 1` are replaced. If `start` and `end` are
omitted, all elements of the source array are replaced.

#### `Array.flat`<a name="flat"></a>
```javascript
const flatArray = nestedArray.flat(flatDegree);
```
This function takes an array containing also sub-arrays and creates a new array where the sub-arrays are concatenated up to a depth of
`flatDegree`. This parameter is optional. If it is omitted, it is set to `1`. The parameter `flatDegree` is a positive number or `Infinity`.
In the latter case, all sub-arrays are concatenated, resulting an array containing all elements in the array and sub-arrays.

#### `Array.from`<a name="from"></a>
```javascript
const newArray = Array.from(iterableItem, mapFn, thisArg)
```
This function creates a new array from an iterable item like a `Set`, a `Map`, or a `NodeList`. Optionally, a callback function for a `map`
and the `this` parameter within this `map` can be provided. The callback function has only the parameters `item` and `index`.

#### `Array.includes`<a name="includes"></a>
```javascript
const isElementInArray = sourceArray.includes(element);
```
This function checks if `element` is one of the elements in the source array. It returns a boolean with the result.

#### `Array.indexOf`<a name="indexof"></a>
```javascript
const index = sourceArray.indexOf(element, startIndex);
```
The function takes the source array and returns the index where the element can be found in the array for the first time. If the element is
not found within the array, `-1` is returned. If not the whole array should be searched, the optional parameter `startIndex` can be set.

#### `Array.isArray`<a name="isarray"></a>
```javascript
const isItAnArray = Array.isArray(elementToBeTested);
```
This function tests if the `elementToBeTested` is an array or not. The function returns a boolean.

#### `Array.join`<a name="join"></a>
```javascript
const combinedString = sourceArray.join(separator);
```
This function takes the elements of the source array and combines them to a string, separated by the optional parameter `separator`. If
`separator` is omitted, a comma (`,`) is used. 

#### `Array.lastIndexOf`<a name="lastindexof"></a>
This function works similar as [Array.indexOf](#indexof), but returns the index of the last element in the array. If the element is not
found within the array, `-1` is returned.

#### `Array.of`<a name="of"></a>
```javascript
const newArray = Array.of(...elements);
```
This function creates a new array including the list of elements passed as parameters. If no elements are passed as parameters, an empty
array is returned.

#### `Array.pop`<a name="pop"></a>
```javascript
const removedElement = sourceArray.pop();
```
This function removes the last element from an array, overwrites the source array, and returns the removed element.

#### `Array.push`<a name="push"></a>
```javascript
const newLength = sourceArray.push(...newElements);
```
This function takes the source array, add `newElements` at the end of the array, overwrites the source array, and returns the length of the
new array.

#### `Array.reverse`<a name="reverse"></a>
```javascript
const reversedArray = sourceArray.reverse();
```
This function takes a source array and returns an array with the same elements in the opposite order.

#### `Array.shift`<a name="shift"></a>
```javascript
const removedElement = sourceArray.shift();
```
This function removes the first element from the source array, overwrites the source array, and returns the removed element.

#### `Array.slice`<a name="slice"></a>
```javascript
const copiedArray = sourceArray.slice(start, end);
```
This function generates a shallow copy of an array or of parts of it. The parameters `start` and `end` are optional: `start` is the first
item to be copied, `end` is the first item that should not be copied. If `end` is omitted the array from `start` to `sourceArray.length - 1`
is copied. If both parameters are omitted, the whole array is copied.

#### `Array.splice`<a name="splice"></a>
```javascript
const removedItems = sourceArray.splice(start, deleteCount, ...items);
```
This function takes the source array, removes `deleteCount` items starting from `start` and inserts `items` instead. An array with the
removed items is returned. After that, the source array is changed. If `deleteCount` is set to `0`, the `items` are just inserted without
removal. The parameters `deleteCount` and `...items` are optional. 

#### `Array.unshift`<a name="unshift"></a>
```javascript
const newLength = sourceArray.unshift(...newElements);
```
This function takes the source array, adds `newElements` at the beginning, overwrites the source array, and returns the number of the
resulting array.

#### `Array.with`<a name="with"></a>
```javascript
const newArray = sourceArray.with(index, newElement);
```
This function takes the source array, replaces `sourceArray[index]` with `newElement`, and returns the resulting array.