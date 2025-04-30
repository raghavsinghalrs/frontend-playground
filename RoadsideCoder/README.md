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

## Now with the same above question want the names who have scored more than 80

```js
const arr = [{name : 'A', rollNumber: 1, marks: 40}, {name : 'B', rollNumber: 2, marks: 100}]

const res = arr.filter(item => item.marks > 40).map(item => item.name);
console.log(res);
```

# Polyfills

##  🚀map
```js
Array.prototype.myMap = function(cb) {
  let arr = [];
  for (let i = 0; i < this.length; i++) {
    arr.push(cb(this[i], i, this));
  }
  return arr;
};
```

## 🚀forEach
```js
Array.prototype.myForEach = function(cb){
    for(let i = 0; i < this.length; i++){
        (cb(this[i], i , this));
    }
}

const arr = [1, 2, 3];
arr.myForEach((item) => console.log(item));
```

## 🚀reduce
```js
Array.prototype.myReduce = function(cb, initialVal = null){
    let accumulator = initialVal;
    let startIndex = 0;
    if(!accumulator){
        accumulator = this[0];
        startIndex = 1
    }
    for(let i = startIndex; i < this.length; i++){
        accumulator = cb(accumulator, this[i], i, this);
    }
    
    return accumulator;
}

const arr = [1, 2, 3];
const data = arr.myReduce((acc, curr) => acc + curr, 0);
console.log(data);
```

