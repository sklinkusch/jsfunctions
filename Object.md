# Object functions

## Table of Contents

1. [Object.assign](#assign)
1. [Object.create](#create)

## `Object.assign`<a name="assign"></a>
```javascript
const resultingObject = Object.assign(targetObject, ...sourceObjects);
```
This function takes a target object, copies the properties from a number of source objects in it (eventually with overwriting), and returns
the resulting object.

## `Object.create`<a name="create"></a>
```javascript
const newObject = Object.create(sourceObject);
```
This function takes the source object and takes it as a model for creating a new object. The new object contains the properties of the
source object (with their respective values) that can be changed after creation.