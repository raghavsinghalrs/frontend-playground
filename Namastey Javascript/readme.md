# Call, Apply and Bind Method

Call Method (function borrowing)

```js
let obj = {
  firstName : 'Raghav',
  lastName : 'Singhal',
  printFullName : function(){
    console.log(this.firstName + " " + this.lastName);
  }
};

let obj2 = {
  firstName : 'X',
  lastName : 'Y',
}

//Here we can use obj printFullName method or we can say borrow it and pass obj2 as a reference.

obj.printFullName(); //Raghav Singhal
obj.printFullName.call(obj2) // X Y
```
```js
//If We separate it

let name = {
  firstName : 'Raghav',
  lastName : 'Singhal',
};

let name2 = {
  firstName : 'X',
  lastName : 'Y',
};

let printFullName = function(){
  console.log(this.firstName + " " + this.lastName);
}

printFullName.call(name); // Raghav Singhal
printFullName.call(name2); // X Y


let printFullName = function(homeTown){
  console.log(this.firstName + " " + this.lastName, hometown);
}
printFullName.call(name, "Morena"); // Raghav Singhal morena
```

Apply method (same as call method, just a difference how we are passing)

```js
let name = {
  firstName : 'Raghav',
  lastName : 'Singhal',
};

let name2 = {
  firstName : 'X',
  lastName : 'Y',
};

let printFullName = function(hometown){
  console.log(this.firstName + " " + this.lastName, hometown);
}

printFullName.apply(name,["morena"]); // Raghav Singhl morena
```

Bind Method

It is similar like call method but it gives us a copy and we can invoke it later.

```js
let res = printFullName.bind(name,"morena");
console.log(res) // function (hometown) { console.log(this.firstName + " " + this.lastName, hometown);}
console.log(res()); // Raghav Singhal morena
```

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

# The Scope Chain, Scope & Lexical Environment 🚀

```js
function a(){
    var a = 10;
    c();
    function c(){
        console.log(a);
    }
}
a();

in hierarchy, c function is lexically inside a, and a is lexically inside global object.

Lexical environment : Local memory + lexical environment of parent And the chain of lexical environment is **scope chain**.
