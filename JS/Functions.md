
## Function Declaration

```js
// Function Declaration 
function walk() {
    console.log('walk');
};
// Anonymous Function Expression
let run = function() {
    console.log('run');
};
let move = run;
run();
move();
```


## Hoisting

Hoisting
Difference - function declaration can be called before it is defined.
Reason - JS engine move all function declaration to top called **Hoisting**.


## Arguments

```js
function sum() {
    let total = 0;
    for (let value of arguments) // can be used any object that have iterator
      total +=value;
    return total;
    // console.log(arguments); // contains all param passed to the function;
    // return a + b; // 1 + undefined(if b not passed as param)
}
console.log(sum(1,2,3,4)); // but we can paas additional arguments (1,2,3,4);
```

In Modern Js we have **Rest Operator**.

### Rest Operator

Used to get multiple argument in JS functions different from spread operator.
```js
function sum(discount,...price) {
    console.log(price); // array of all elements
    const total = price.reduce((a, b) => a + b);
    return total * (1 - discount);
}
  
console.log(sum(0.1, 1, 2, 3, 4, 5));
```

- We can pass any number of arguments before the rest operator but not after that's the reason this operator is called rest.


## Default Value

```js
function interest(principal, rate = 3.5, years) {
    return principal * rate / 100 * years;
}
// once we define default value to param then next param should have default.
// trick to  pass this case by setting undefined in default param then we can pass next param
// but this is not good code so make sure you set default parameters is the last parameter in list
console.log(interest(10000, undefined, 5));
```

## Getters and Setters

```js
const person = {
    firstName: 'DevilX',
    lastName: 'Fiero',
    get fullName() {
        return `${person.firstName} ${person.lastName}`;
    },
    set fullName(value) {
        const parts = value.split(' ');
        this.firstName = parts[0];
        this.lastName = parts[1];
    }
};

// getters => access properties
// setters => change (mutate) them
console.log(person.fullName);
```

## Try and Catch

When we have simple error object defined it is and error but when we throw that error it becomes exception.

```js
const person = {
    firstName: 'DevilX',
    lastName: 'Fiero',
    get fullName() {
        return `${person.firstName} ${person.lastName}`;
    },
    set fullName(value) {
        if (typeof value !== 'string') 
          throw new Error('Value is not a string');

        const parts = value.split(' ');
        if (parts.length !== 2)
          throw new Error('Enter a first and last name');
        this.firstName = parts[0];
        this.lastName = parts[1];
    }
};

try {
    person.fullName = '';
}
catch (e) {
    alert(e);
}
```

## Local vs Global Scope

Local - Variables defined in a code block and accessible inside that only. If we have same var global and local precedence will be given to local variable.

Global - Variables define globally can be accessible by any of the code block.

### let vs var 
when you declare var its scope is not limited to the block in which it's defined its limited to the function.
var => function-scoped
ES6 (ES2015) : let, const => block-scoped

- Var also add global variable to the window object.
- Functions defined globally also get added to window object . Modules are used to prevent this



## The 'this' keyword

The **object** that is executing the current function.

method -> obj
global functions -> this by default references the global object (window, global)
but if we use constructor function using new this references to empty object.

this inside call back function references to window object as callback function are global not a method inside object.

```js
const video = {
    title: 'a',
    tags: ['a', 'b', 'c'],
    showTags() {
        this.tags.forEach(function(tag) {
            console.log(this.title, tag);
        }, this); // second param is this object we want to specify.
    }
};
video.showTags();
```


## Change This

1. const self = this and then use self.
2. 
```js
// by using bind method
function playVideo(a, b) {
    console.log(this);
}

playVideo.call({ name: 'DevilXfiero'}, 1, 2);
playVideo.apply({ name: 'DevilXfiero'}, [1, 2]);
playVideo.bind({ name: 'DevilXfiero'})();
```

3. Arrow Function - Inherit this value.
