# Javascript functions

This is a collection of useful Javascript functions for different types.

## Table of Contents
1. [Array functions](#array)
   1. [Loop-based functions](#array-loop)
      1. [Array.forEach](#forEach)
      1. [Array.map](#map)
      1. [Array.filter](#filter)
      1. [Array.find](#find)
      1. [Array.findIndex](#findindex)
      1. [Array.reduce](#reduce)

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
condition given in the callback function. Thus, a boolean has to be returned inside the callback function.

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