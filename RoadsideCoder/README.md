# Map vs forEach difference 

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
