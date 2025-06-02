# DEbouncing && throttling

```js
let a = document.querySelector('.incr-val');
let b = document.querySelector('.trigg-val');

var count1 = 0, count2 = 0;

// const debounce = (cb, delay) => {
//     let timeoutId;
//     return function(...args){
//         if(timeoutId) clearTimeout(timeoutId);
//         timeoutId = setTimeout(()=>{
//             cb(...args);
//         },delay);
//     }
// }

// const debounceEffect = debounce(() => {
//     count2++;
//     b.innerHTML = count2;
// }, 800)

const throttle = (cb, delay) => {
    let last = 0;
    return (...args) => {
        let now = new Date().getTime();
        if(now-last < delay) return;
        last = now;
        cb(...args);
    }
}

const throttleEffect = throttle(() => {
    count2++;
    b.innerHTML = count2;
},1000)

const incrementBtn = document.querySelector('.increment-btn');
incrementBtn.addEventListener('click', () => {
    a.innerHTML = ++count1;
    // debounceEffect();
    throttleEffect();
})
```
