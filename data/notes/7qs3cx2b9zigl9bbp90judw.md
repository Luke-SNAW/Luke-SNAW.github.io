
https://blog.bitsrc.io/common-javascript-interview-question-what-is-the-purpose-of-this-e9f5e11720c5

**In JavaScript, “this” will refer to the execution context for that specific call.**

**What does that mean?**

**When we invoke a function, an execution context is created.** This execution context is basically a record of information that is important to our function. It lets us know where the function was called from, the parameters that were passed etc. **One of the most important properties the record saves is ‘this’ reference which will be used during the function’s execution.**

**But what will ‘this’ reference?**

Well, in order to determine this, we will need to find exactly where our function was called from. Once we find the location, there are some rules that are applicable.

Rules:

# 1. New binding

When a function is invoked with the new keyword, ‘this’ will reference the newly created object:

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person1 = new Person("Peter", 55);
// the new binding allows us to assign this to the object we instantiate
```

# 2. Implicit binding

When a function is invoked with the dot notation, ‘this’ will reference the object to the left of our dot:

```javascript
const person = {
  name: "Thomas",
  age: 40,
  hi() {
    console.log("Hi, " + this.name);
  },
};
person.hi(); // Hi, Thomas
```

# 3. Explicit binding

Uses call, apply and bind functions to explicitly provide value of ‘this’. These methods allow a method that was defined for one object, to be assigned and called by another object.

Thus explicitly providing the value of ‘this’:

```javascript
let cat = {
  name: "Bob",
  age: 5,
  type: "Cat",
};

let animal = {
  animalInfo: function (food) {
    return `Our ${this.type}, ${this.name}, is ${this.age} years old. He likes to eat ${food}`;
  },
};

console.log(animal.animalInfo.call(cat, "fish"));
// Our Cat, Bob, is 5 years old. He likes to eat fish

console.log(animal.animalInfo.apply(cat, ["fish"]));
// Our Cat, Bob, is 5 years old. He likes to eat fish

const bound = animal.animalInfo.bind(cat);
console.log(bound("rats"));
// Our Cat, Bob, is 5 years old. He likes to eat rats
```

# 4. Default binding

Undefined in strict mode, otherwise the global object — even if used within a function:

```javascript
console.log(this); // undefined

function myFunc() {
  console.log(this); // undefined
}
myFunc();
```

# 5. Event Listeners

When using event listeners, the object being listened to will be bound to ‘this’:

```javascript
const myBtn = document.getElementById("myBtn");

myBtn.addEventlistener("click", myFunc);

function myFunc() {
  // would bind button to `this` in side of myBtn
  console.log(this);
}
```

# 6. Lexical binding with arrow functions

Arrow functions bind this lexically. Since they don’t have their own context in which they execute, ‘this’ get inherited from the parent function:

```javascript
const person = {
  name: "Jon Snow",
  sayHi: function () {
    console.log(this.name, "says hi");
  },
};

person.sayHi(); // Jon Snow says sayHi

const person2 = {
  name: "Jon Snow",
  sayHi: () => {
    console.log(this.name, "says hi");
  },
};

person2.sayHi(); // undefined says hi
```
