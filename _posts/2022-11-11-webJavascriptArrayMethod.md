---
title: "[Web] 자바스크립트 배열 함수"

sidebar:
    nav: "web"
---

<br/>

# 1. forEach

array의 요소를 하나씩 읽어오는 반복문이다.

## (1) 문법

```javascript
// Arrow function
Array.forEach((element) => { /* … */ })
Array.forEach((element, index) => { /* … */ })
Array.forEach((element, index, array) => { /* … */ })

// Callback function
Array.forEach(callbackFn)
Array.forEach(callbackFn, thisArg)

// Inline callback function
Array.forEach(function (element) { /* … */ })
Array.forEach(function (element, index) { /* … */ })
Array.forEach(function (element, index, array) { /* … */ })
Array.forEach(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
const arraySparse = [1, 3, 7];

arraySparse.forEach((element) => {
  console.log({ element });
});

// { element: 1 }
// { element: 3 }
// { element: 7 }
```

### b. index 사용 예시

```javascript
const logArrayElements = (element, index) => {
  console.log(`a[${index}] = ${element}`);
};

// Notice that index 2 is skipped, since there is no item at
// that position in the array.
[2, 5, , 9].forEach(logArrayElements);
// Logs:
// a[0] = 2
// a[1] = 5
// a[3] = 9
```

### c. thisArg 사용 예시

```javascript
class Counter {
  constructor() {
    this.sum = 0;
    this.count = 0;
  }
  add(array) {
    // Only function expressions will have its own this binding
    array.forEach(function countEntry(entry) {
      this.sum += entry;
      ++this.count;
    }, this);
  }
}

const obj = new Counter();
obj.add([2, 5, 9]);
console.log(obj.count); // 3
console.log(obj.sum); // 16
```

<br/>


# 2. map

array의 요소를 하나씩 수정하여 새로운 array를 만드는 반복문이다.

## (1) 문법

```javascript
// Arrow function
const newArray = Array.map((element) => { /* … */ })
const newArray = Array.map((element, index) => { /* … */ })
const newArray = Array.map((element, index, array) => { /* … */ })

// Callback function
const newArray = Array.map(callbackFn)
const newArray = Array.map(callbackFn, thisArg)

// Inline callback function
const newArray = Array.map(function (element) { /* … */ })
const newArray = Array.map(function (element, index) { /* … */ })
const newArray = Array.map(function (element, index, array) { /* … */ })
const newArray = Array.map(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
const numbers = [1, 4, 9];
const roots = numbers.map((num) => Math.sqrt(num));

// roots is now     [1, 2, 3]
// numbers is still [1, 4, 9]
```

### b. index 사용 예시 

```javascript
console.log(
  [1, , 3].map((x, index) => {
    console.log(`Visit ${index}`);
    return x * 2;
  })
);
// Visit 0
// Visit 2
// [2, empty, 6]
```

<br/>


# 3. filter

array의 요소를 하나씩 읽어와서 조건을 만족하는 요소로 구성된 새로운 array를 만드는 반복문이다.

## (1) 문법

```javascript
// Arrow function
const newArray = Array.filter((element) => { /* … */ })
const newArray = Array.filter((element, index) => { /* … */ })
const newArray = Array.filter((element, index, array) => { /* … */ })

// Callback function
const newArray = Array.filter(callbackFn)
const newArray = Array.filter(callbackFn, thisArg)

// Inline callback function
const newArray = Array.filter(function (element) { /* … */ })
const newArray = Array.filter(function (element, index) { /* … */ })
const newArray = Array.filter(function (element, index, array) { /* … */ })
const newArray = Array.filter(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
function isBigEnough(value) {
  return value >= 10;
}

const filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]
```

### b. array파라미터 사용 예시

```javascript
// Modifying each word
let words = ['spray', 'limit', 'exuberant', 'destruction', 'elite', 'present'];

const modifiedWords = words.filter((word, index, arr) => {
  arr[index + 1] += ' extra';
  return word.length < 6;
});

console.log(modifiedWords);
// Notice there are three words below length 6, but since they've been modified one is returned
// ["spray"]

// Appending new words
words = ['spray', 'limit', 'exuberant', 'destruction', 'elite', 'present'];
const appendedWords = words.filter((word, index, arr) => {
  arr.push('new');
  return word.length < 6;
})

console.log(appendedWords);
// Only three fits the condition even though the `words` itself now has a lot more words with character length less than 6
// ["spray" ,"limit" ,"elite"]

// Deleting words
words = ['spray', 'limit', 'exuberant', 'destruction', 'elite', 'present'];
const deleteWords = words.filter((word, index, arr) => {
  arr.pop();
  return word.length < 6;
})

console.log(deleteWords);
// Notice 'elite' is not even obtained as it's been popped off 'words' before filter can even get there
// ["spray" ,"limit"]
```

<br/>


# 4. some

array 요소 중에 조건문을 만족하는 요소가 하나라도 있으면 `true` 출력, 아니면 `false` 출력하는 반복문이다.

## (1) 문법

```javascript
// Arrow function
const true_false_result = Array.some((element) => { /* … */ })
const true_false_result = Array.some((element, index) => { /* … */ })
const true_false_result = Array.some((element, index, array) => { /* … */ })

// Callback function
const true_false_result = Array.some(callbackFn)
const true_false_result = Array.some(callbackFn, thisArg)

// Inline callback function
const true_false_result = Array.some(function (element) { /* … */ })
const true_false_result = Array.some(function (element, index) { /* … */ })
const true_false_result = Array.some(function (element, index, array) { /* … */ })
const true_false_result = Array.some(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
function isBiggerThan10(element, index, array) {
  return element > 10;
}

[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true

[2, 5, 8, 1, 4].some((x) => x > 10);  // false
[12, 5, 8, 1, 4].some((x) => x > 10); // true

const fruits = ['apple', 'banana', 'mango', 'guava'];

function checkAvailability(arr, val) {
  return arr.some((arrVal) => val === arrVal);
}

checkAvailability(fruits, 'kela');   // false
checkAvailability(fruits, 'banana'); // true
```

<br/>


# 5. every

array 요소가 모두 조건문을 만족하면 `true` 출력, 아니면 `false` 출력하는 반복문이다.

## (1) 문법

```javascript
// Arrow function
const true_false_result = Array.every((element) => { /* … */ })
const true_false_result = Array.every((element, index) => { /* … */ })
const true_false_result = Array.every((element, index, array) => { /* … */ })

// Callback function
const true_false_result = Array.every(callbackFn)
const true_false_result = Array.every(callbackFn, thisArg)

// Inline callback function
const true_false_result = Array.every(function (element) { /* … */ })
const true_false_result = Array.every(function (element, index) { /* … */ })
const true_false_result = Array.every(function (element, index, array) { /* … */ })
const true_false_result = Array.every(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
function isBigEnough(element, index, array) {
  return element >= 10;
}
[12, 5, 8, 130, 44].every(isBigEnough);   // false
[12, 54, 18, 130, 44].every(isBigEnough); // true

const isSubset = (array1, array2) => array2.every((element) => array1.includes(element));

console.log(isSubset([1, 2, 3, 4, 5, 6, 7], [5, 7, 6])); // true
console.log(isSubset([1, 2, 3, 4, 5, 6, 7], [5, 8, 7])); // false
```

<br/>


# 6. find

array 요소 중에 조건문을 만족하는 첫 요소를 반환한다.

만족하는 요소가 없으면 `undefined`를 반환한다.

## (1) 문법

```javascript
// Arrow function
const true_false_result = Array.find((element) => { /* … */ })
const true_false_result = Array.find((element, index) => { /* … */ })
const true_false_result = Array.find((element, index, array) => { /* … */ })

// Callback function
const true_false_result = Array.find(callbackFn)
const true_false_result = Array.find(callbackFn, thisArg)

// Inline callback function
const true_false_result = Array.find(function (element) { /* … */ })
const true_false_result = Array.find(function (element, index) { /* … */ })
const true_false_result = Array.find(function (element, index, array) { /* … */ })
const true_false_result = Array.find(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 },
];

function isCherries(fruit) {
  return fruit.name === "cherries";
}

console.log(inventory.find(isCherries));
// { name: 'cherries', quantity: 5 }

const result = inventory.find(({ name }) => name === "cherries");
console.log(result); // { name: 'cherries', quantity: 5 }
```

<br/>


# 7. findIndex

array 요소 중에 조건문을 만족하는 첫 요소의 index를 반환한다.

만족하는 요소가 없으면 `-1`을 반환한다.

## (1) 문법

```javascript
// Arrow function
const true_false_result = Array.findIndex((element) => { /* … */ })
const true_false_result = Array.findIndex((element, index) => { /* … */ })
const true_false_result = Array.findIndex((element, index, array) => { /* … */ })

// Callback function
const true_false_result = Array.findIndex(callbackFn)
const true_false_result = Array.findIndex(callbackFn, thisArg)

// Inline callback function
const true_false_result = Array.findIndex(function (element) { /* … */ })
const true_false_result = Array.findIndex(function (element, index) { /* … */ })
const true_false_result = Array.findIndex(function (element, index, array) { /* … */ })
const true_false_result = Array.findIndex(function (element, index, array) { /* … */ }, thisArg)
```

## (2) 예시

### a. 기본 사용 예시

```javascript
function isPrime(element) {
  if (element % 2 === 0 || element < 2) {
    return false;
  }
  for (let factor = 3; factor <= Math.sqrt(element); factor += 2) {
    if (element % factor === 0) {
      return false;
    }
  }
  return true;
}

console.log([4, 6, 8, 9, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 9, 12].findIndex(isPrime)); // 2 (array[2] is 7)
```

<br/>