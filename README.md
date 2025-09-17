# javascript_pre_2025

Array polyfill method

Nice start 👍 Let’s refine your **`forEach` polyfill** a bit.

The native **`forEach`** method in JavaScript works like this:

* Iterates over all elements in the array.
* Calls the callback with three arguments:

  1. current element
  2. index
  3. the original array
* Skips **holes** in sparse arrays.
* Does **not return anything** (returns `undefined`).
* The callback runs with an optional `thisArg`.

Here’s a closer-to-native polyfill:

```javascript
// Polyfill for forEach
if (!Array.prototype.ourForEach) {
  Array.prototype.ourForEach = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError("Array.prototype.ourForEach called on null or undefined");
    }
    if (typeof callback !== "function") {
      throw new TypeError(callback + " is not a function");
    }

    const arr = Object(this);
    const len = arr.length >>> 0; // convert to uint32

    for (let i = 0; i < len; i++) {
      if (i in arr) { // skip holes
        callback.call(thisArg, arr[i], i, arr);
      }
    }
  };
}

// Example usage
const names = ["Hari", "Mohan", "Prajapat"];

function consoleFunc(name, index, array) {
  console.log(`Index ${index}: ${name}`, array);
}

names.ourForEach(consoleFunc);
```

✅ This now behaves much like the **native `forEach`**.


Nice start 👍 Let’s refine your **`forEach` polyfill** a bit.

The native **`forEach`** method in JavaScript works like this:

* Iterates over all elements in the array.
* Calls the callback with three arguments:

  1. current element
  2. index
  3. the original array
* Skips **holes** in sparse arrays.
* Does **not return anything** (returns `undefined`).
* The callback runs with an optional `thisArg`.

Here’s a closer-to-native polyfill:

```javascript
// Polyfill for forEach
if (!Array.prototype.ourForEach) {
  Array.prototype.ourForEach = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError("Array.prototype.ourForEach called on null or undefined");
    }
    if (typeof callback !== "function") {
      throw new TypeError(callback + " is not a function");
    }

    const arr = Object(this);
    const len = arr.length >>> 0; // convert to uint32

    for (let i = 0; i < len; i++) {
      if (i in arr) { // skip holes
        callback.call(thisArg, arr[i], i, arr);
      }
    }
  };
}

// Example usage
const names = ["Hari", "Mohan", "Prajapat"];

function consoleFunc(name, index, array) {
  console.log(`Index ${index}: ${name}`, array);
}

names.ourForEach(consoleFunc);
```

✅ This now behaves much like the **native `forEach`**.




