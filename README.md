# Javascript functions

This is a collection of useful Javascript functions for different types.

## Array functions

In the following functions, the parameters `index` and `array` are optional.
They should be only used if these values are necessary within the callback function.

### `Array.forEach`
```
Array.forEach((item, index, array) => {
  // do some stuff
});
```
This function is just a replacement for a `while` or `for` loop. Inside the
callback, there is no return statement.

### `Array.map`
```
const newArray = Array.map((item, index, array) => {
  // do some stuff
  return anything;
});
```
This function takes the array and returns an array of equal size. A return
statement in the callback function is required.

### `Array.filter`
```
const newArray = Array.filter((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
});
```
This function takes the array and returns an array with all elements whose
elements match a condition. Inside the callback function, a boolean has to be
returned.

### `Array.find`
```
const firstMatchingItem = Array.find((item, index, array) => {
  // do some stuff
  return boolean; // (true or false)
});
```
This function takes the array and returns the first element that matches a
condition. Inside the callback function, a boolean has to be returned.