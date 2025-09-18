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


Perfect 👍 Let’s go through **practical examples** of `reduce()` so you can easily explain them in an interview.

---

## 🔹 Basic Examples of `reduce()`

```js
const arr = [1, 2, 3, 4];
```

### 1. Sum of array

```js
const sum = arr.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

👉 Explanation:

* Start with `0`
* `0 + 1 = 1`
* `1 + 2 = 3`
* `3 + 3 = 6`
* `6 + 4 = 10`

---

### 2. Product of array

```js
const product = arr.reduce((acc, num) => acc * num, 1);
console.log(product); // 24
```

---

### 3. Find maximum value

```js
const max = arr.reduce((acc, num) => (num > acc ? num : acc));
console.log(max); // 4
```

---

## 🔹 Advanced Examples

### 4. Flatten an array

```js
const nested = [[1, 2], [3, 4], [5]];
const flat = nested.reduce((acc, el) => acc.concat(el), []);
console.log(flat); // [1, 2, 3, 4, 5]
```

---

### 5. Count frequency of elements

```js
const fruits = ["apple", "banana", "apple", "orange", "banana", "apple"];

const freq = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});

console.log(freq); 
// { apple: 3, banana: 2, orange: 1 }
```

---

### 6. Group objects by property

```js
const people = [
  { name: "Hari", age: 25 },
  { name: "Mohan", age: 25 },
  { name: "Ravi", age: 30 },
];

const grouped = people.reduce((acc, person) => {
  (acc[person.age] = acc[person.age] || []).push(person.name);
  return acc;
}, {});

console.log(grouped);
// { 25: ["Hari", "Mohan"], 30: ["Ravi"] }
```

---

### 7. Remove duplicates

```js
const nums = [1, 2, 2, 3, 4, 4, 5];

const unique = nums.reduce((acc, num) => {
  if (!acc.includes(num)) acc.push(num);
  return acc;
}, []);

console.log(unique); // [1, 2, 3, 4, 5]
```

---

✅ These examples cover **math, array flattening, frequency counting, grouping, and deduplication** → the most common interview-style questions for `reduce`.

---

Do you want me to also **write these same examples using your polyfill (`myReduce`)** so you can show both native and custom versions in your interview?


    Array.prototype.myReduce = function (callback, initialValue) {

        // Variable that accumulates the result
        // after performing operation one-by-one
        // on the array elements
        let accumulator = initialValue;

        for (let i = 0; i < this.length; i++) {
            
            // If the initialValue exists, we call
            // the callback function on the existing
            // element and store in accumulator
            if (accumulator) {
                accumulator = callback.call(undefined, 
                    accumulator, this[i], i, this);
                
                // If initialValue does not exist, 
                // we assign accumulator to the
                // current element of the array
            }
            else {
                accumulator = this[i];
            }
        }

        // We return the overall accumulated response
        return accumulator;
    }

    // Code to calculate sum of array elements
    // using our own reduce method
    const arr = [1, 2, 3, 4];
    console.log(arr.myReduce((total, elem) => total + elem));

    // Code to calculate multiplication of all array elements
    console.log(arr.myReduce((prod, elem) => prod * elem));







