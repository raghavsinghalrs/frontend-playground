# Pollyfill for Bind

```js
let name = {
    firstName : 'Raghav',
    LastName : 'Singhal'
}

//Bind method

let printName = function(args, city){
    console.log(args, this.firstName + " " + this.LastName, city);
}

let printMyName = printName.bind(name, "Hello");
printMyName("Morena");


// Pollyfill of bind method
Function.prototype.myBind = function(...args){
    let obj = this;
    let params = args.slice(1);
    return function(...args2){
        obj.apply(args[0], [...params, ...args2]);
    }
}

let printMyName2 = printName.myBind(name, "Hello");
printMyName2("Morena");
```
# Function currying

It includes concept of bind and closures.

```js
//Using bind method it will make a copy of multiply function and we are passing the values.

const multiply = (x,y) => {
    console.log(x*y);
}

const multiplyBy2 = multiply.bind(this,2);
multiplyBy2(3);

const multiplyBy3 = multiply.bind(this,3);
multiplyBy3(4);
```

```js
// using closure concept

let multiply = function(x){
    return function(y){
        console.log(x*y);
    }
}

let multiplyBy2 = multiply(2);
multiplyBy2(3);
```
