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


