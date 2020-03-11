```javascript 
// ARRAY METHODS

/* 
    1. Array.from() - creates a new, shallow-copied Array instance from an array-like or iterable object. 
    -- Array.from(arrayLike [, mapFn [, thisArg]]) --
*/

console.log(Array.from('foo')); // expected output: Array ["f", "o", "o"]
console.log(Array.from([1, 2, 3], x => x + x)); // expected output: Array [2, 4, 6]
////////////////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    2.Array.isArray() - determines whether the passed value is an Array.
    -- Array.isArray(value) --
*/

Array.isArray([1, 2, 3]);  // true
Array.isArray({foo: 123}); // false
Array.isArray('foobar');   // false
Array.isArray(undefined);  // false
////////////////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    3.Array.of() - creates a new Array instance from a variable number of arguments, regardless of number or type of the arguments.
    -- Array.of(element0[, element1[, ...[, elementN]]]) --

    Details:
    The difference between Array.of() and the Array constructor is in the handling of integer arguments: Array.of(7) creates an array with a single element, 7, whereas Array(7) creates an empty array with a length property of 7 (Note: this implies an array of 7 empty slots, not slots with actual undefined values).
*/
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]

Array(7);          // array of 7 empty slots
Array(1, 2, 3);    // [1, 2, 3]
////////////////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    4.Array.prototype.concat() -  is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
    -- const new_array = old_array.concat([value1[, value2[, ...[, valueN]]]]) -- RETURNS NEW ARRAY

    Details:
    The concat method creates a new array consisting of the elements in the object on which it is called, followed in order by, for each argument, the elements of that argument (if the argument is an array) or the argument itself (if the argument is not an array). It does not recurse into nested array arguments.
*/

// Concatenating two arrays
const letters = ['a', 'b', 'c'];
const numbers = [1, 2, 3];

letters.concat(numbers);
// result in ['a', 'b', 'c', 1, 2, 3]


// Concatenating three arrays
const num1 = [1, 2, 3];
const num2 = [4, 5, 6];
const num3 = [7, 8, 9];

const numbers = num1.concat(num2, num3);

console.log(numbers); 
// results in [1, 2, 3, 4, 5, 6, 7, 8, 9]


// Concatenating values to an array
const letters = ['a', 'b', 'c'];
const alphaNumeric = letters.concat(1, [2, 3]);

console.log(alphaNumeric); // results in ['a', 'b', 'c', 1, 2, 3]


// Concatenating nested arrays
const num1 = [[1]];
const num2 = [2, [3]];
const numbers = num1.concat(num2);

console.log(numbers); // results in [[1], 2, [3]]

// modify the first element of num1
num1[0].push(4);
console.log(numbers); // results in [[1, 4], 2, [3]]
////////////////////////////////////////////////////////////////////////////////////////////////////////////


/* 
    5.Array.entries()

    Details:
    The entries() method returns a new Array Iterator object that contains the key/value pairs for each index in the array.
*/
const array1 = ['a', 'b', 'c'];

const iterator1 = array1.entries();

console.log(iterator1.next().value);
// expected output: Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]


// ==== Iterating with index and element ====
const a = ['a', 'b', 'c'];

for (const [index, element] of a.entries())
  console.log(index, element);

// 0 'a' 
// 1 'b' 
// 2 'c'

// ==== Using a for…of loop ====
var a = ['a', 'b', 'c'];
var iterator = a.entries();

for (let e of iterator) {
  console.log(e);
}
// [0, 'a']
// [1, 'b']
// [2, 'c'] 
////////////////////////////////////////////////////////////////////////////////////////////

/* 
    6.Array.fill()
    -- arr.fill(value[, start[, end]]) -- RETURNS MODIFIED ARRAY

    Details:
    The fill() method changes all elements in an array to a static value, from a start index (default 0) to an end index (default array.length). It returns the modified array.
    HAS POLYFILL
*/

const array1 = [1, 2, 3, 4];

// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]

// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]

////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    7.Array.filter()
    -- let newArray = arr.filter(callback(element[, index, [array]])[, thisArg]) -- RETURNS NEW ARRAY

    Details:
    The filter() method creates a new array with all elements that pass the test implemented by the provided function.
*/

const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

////////////////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    8.Array.find()
    -- arr.find(callback(element[, index[, array]])[, thisArg]) -- 

    Details:
    The find() method returns the value of the first element in the provided array that satisfies the provided testing function.

    If you need the index of the found element in the array, use findIndex().
    If you need to find the index of a value, use Array.prototype.indexOf(). (It’s similar to findIndex(), but checks each element for equality with the value instead of using a testing function.)
    If you need to find if a value exists in an array, use Array.prototype.includes().
    If you need to find if any element satisfies the provided testing function, use Array.prototype.some().
*/

const array1 = [5, 12, 8, 130, 44];
const found = array1.find(element => element > 10);
console.log(found);
// expected output: 12

//////////////////////////////////////////////////////////////////////////////////////////////////////////////


/* 
    8.Array.findIndex()
    -- arr.findIndex(callback( element[, index[, array]] )[, thisArg]) -- 

    Details:
    The findIndex() method returns the index of the first element in the array that satisfies the provided testing function. Otherwise, it returns -1, indicating that no element passed the test.
    HAS POLYFILL
*/

const array1 = [5, 12, 8, 130, 44];
const isLargeNumber = (element) => element > 13;
console.log(array1.findIndex(isLargeNumber));
// expected output: 3

////////////////////////////////////////////////////////////////////////////////////////////////////////////

/* 
    9.Array.flat()
    -- var newArray = arr.flat([depth]); -- 

    Details:
    The flat() method creates a new array with all sub-array elements concatenated into it recursively up to the specified depth.
*/

// ==== Flattening nested arrays ====
const arr1 = [1, 2, [3, 4]];
arr1.flat(); 
// [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// ===== Flattening and array holes ======
// --- The flat method removes empty slots in arrays: ---

const arr5 = [1, 2, , 4, 5];
arr5.flat();
// [1, 2, 4, 5]

////////////////////////////////////////////////////////////////////////////////////////////////////////////
```



<!--  APPENDIX
1. Array like object - An Object which has a length property of a non-negative Integer, and usually some indexed properties

 -->