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


map in JavaScript

What is map?

The map() method creates a new array populated with the results of calling a provided function on every element.

Unlike forEach, it returns a new array.

Does not mutate the original array (unless the callback itself mutates elements).

🔹 Syntax
array.map(callback(currentValue, index, array), thisArg)

Parameters:

callback → Function executed on each element.

currentValue → The element being processed.

index (optional) → Index of element.

array (optional) → The whole array.

thisArg → Optional value to use as this inside the callback.

🔹 Example
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(num => num * 2);

console.log(doubled); // [2, 4, 6, 8]
console.log(numbers); // [1, 2, 3, 4] (original unchanged)




```javascript
Array.prototype.ourMap = function(callback) {
  const result = [];
  for (let i = 0; i < this.length; i++) {
    result.push(callback(this[i], i, this));
  }
  return result;
};

// Example
const numbers = [1, 2, 3, 4];
const doubled = numbers.ourMap(num => num * 2);

console.log(doubled); // [2, 4, 6, 8]
```

---

✅ This works like `map`:

* Iterates over each element.
* Runs the callback with `(element, index, array)`.
* Collects results in a new array.






