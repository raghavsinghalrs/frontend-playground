# Map, forEach, reduce 

## Difference in returning as map returns the new array while forEach modifies the original array

```js
const arr = [1,2,3,4]

const mapRes = arr.map(item => item + 3);
const forEachRes = arr.forEach(item => item + 3);

console.log(mapRes); // [4,5,6,7];
console.log(forEachRes); // undefined (it will not return anything)

//But if we have to change anything then
const forEachRes = arr.forEach((item, index) => {
    arr[index] = item + 3;
});

console.log(arr); // [4,5,6,7] Modifies the original array
```

## In map we can chaining difference functions

```js
const arr = [1,2,3,4]

const mapRes = arr.map(item => item + 3).filter();
```

## Reduce example

```js
let arr = [{name : 'A', rollNumber: 1, marks: 40}, {name : 'B', rollNumber: 2, marks: 100}]
const sum = arr.reduce((acc,curr) => acc + curr.marks, 0);
console.log(sum);

```


