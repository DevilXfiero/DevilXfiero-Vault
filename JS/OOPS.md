
- # Encapsulation
- # Abstraction
- # Inheritance
- # Polymorphism



## Abstraction

scope - variables declared inside the function that dies after the execution of function

closure - variable that function has access to and preserve their state(memory) even after function execute are within closure of function.

```js
function Circle(radius) {
    this.radius = radius;
    let defaultLocation = {x: 0, y: 0}; // to hide members from the outside
    let  computeOptimumLocation = function(factor) {

    }
    this.draw = function() {
        computeOptimumLocation(0.1);
        console.log('draw');
    }
}
```


## Getter and Setter 

```js
function Circle(radius) {
    this.radius = radius;
    let defaultLocation = {x: 0, y: 0}; // to hide members from the outside
    let  computeOptimumLocation = function(factor) {

    }
    this.draw = function() {
        computeOptimumLocation(0.1);
        console.log('draw');
    };
    // can be accessed as method
    this.getDefaultLocation = function() {
        return defaultLocation;
    };
    // if we want as property
    // use to define getter and setter for private property 
    // first param - object, second pararm - name of property, third param object key value pair get and set
    Object.defineProperty(this, 'defaultLocation', {
        get: function() {
            return defaultLocation;
        },
        set: function(value) {
            if (!value.x || !value.y) 
              throw new Error('Invalid location.');
            defaultLocation = value;
        }
    })

}
const circle = new Circle(10);
circle.defaultLocation = {x: 10, y:5};
console.log(circle.defaultLocation);
```


# Inheritance

In JS we don't have classes only objects.

Classical vs Prototypical Inheritance

## Prototype - parent of another object.

 every object we create in JS directly or indirectly inherits from ObjectBase (just name given) except the root object.

```js
let x = {};
let y = {};

console.log(Object.getPrototypeOf(x) === Object.getPrototypeOf(y));
```


### Multilevel Inheritance

objectBase <--- arrayBase <--- myArray

Objects created by a given constructor will have the same prototype.


## Property Descriptors

```js
let person = {name: 'DevilXfiero'};
let objectBase = Object.getPrototypeOf(person);
let descriptor = Object.getOwnPropertyDescriptor(objectBase, 'toString');
console.log(descriptor);

// Output
// {
//     value: [Function: toString],
//     writable: true,
//     enumerable: false,
//     configurable: true
// }

Object.defineProperty(person, 'name',{
    writable: false,
    enumerable: false,
    configurable: false
});

person.name = 'John'; // writable  name not set 
console.log(Object.keys(person)); // get empty array
delete person.name //not delete this propery 
```

### Constructor Prototype

Prototype of constructor used to create that object will be same as prototype of the Object.

```js
let obj = {}; // constructor new Object()
console.log(obj.__proto__ === Object.prototype);
```

## Prototypes vs. Instance Members

We can access instance members from prototype members and vice versa and also can override prototype members for current object. e.g toString()

```js
function Circle(radius) {
    // Instance members
    this.radius = radius;

    this.move = function() {
        this.draw();
        console.log('move');
    }
}

Circle.prototype.draw = function() {
    console.log('draw');
}
const c1 = new Circle(1);
const c2 = new Circle(2);

Circle.prototype.toString = function() {
    return 'Circle with radius ' + this.radius;
}
console.log(c1.toString());
console.log(c2.toString());
```

## Iterating Instance and Prototype members

```js
// Returns instace members
console.log(Object.keys(c1));

// Returns all members (instance(own) + prototype)
for (let key in c1) console.log(key);
c1.hasOwnProperty('radius'); // to check instance and prototype property 
```

## Avoid Extending  the Built-in Objects

Don't modify objects you don't own!

# [[Prototypical Inheritance]]


## Polymorphism

```js
function extend(Child, Parent) {
    Child.prototype = Object.create(Parent.prototype); 
    Child.prototype.constructor = Child;
}
function Shape(color) {
    this.color = color;

}
Shape.prototype.duplicate = function() {
    console.log('duplicate');
}

function Circle(radius) {
    this.radius = radius;
}
extend(Circle, Shape);
Circle.prototype.duplicate = function() {
    console.log('duplicate circle');
}

function Square(size) {
    this.size = size;
}
extend(Square, Shape);
Square.prototype.duplicate = function() {
    console.log('duplicate square');
}

const shapes = [
    new Circle(),
    new Square()
];

for (let shape of shapes) {
    shape.duplicate();
}
```

> [!Info] Avoid creating inheritance hierarchies
> Favour Composition over Inheritance

## Get methods of instance of parent class

```js
function HtmlElement() {
    this.click = function() {
        console.log('clicked');
    }
}

HtmlElement.prototype.focus = function() {
    console.log('focused');
}

function HtmlSelectElement(items = []) {
    this.items = items;

    this.addItem= function(item) {
        this.items.push(item);
    }

    this.removeItem = function(item) {
        this.items.splice(this.items.indexOf(item), 1);
    }
};

// HtmlSelectElement.prototype = Object.create(HtmlElement.prototype); // will only contains prototype method focus not instance method click
HtmlSelectElement.prototype = new HtmlElement();// this will have both method
HtmlSelectElement.prototype.constructor = HtmlSelectElement;

```


## Mixins or Composition

```js
function mixin(target, ...sources) { 
    Object.assign(target, ...sources); 
} 

const canEat = {
    eat: function() {
        this.hunger--;
        console.log('eating');
    }
};

const canWalk = {
    walk: function() {
        console.log('walking');
    }
};

const canSwim = {
    swim: function() {
        console.log('swim');
    }
}

function Person() {
}

mixin(Person.prototype, canEat, canWalk);
const person = new Person();
console.log(person);


function GoldFish() {
}

mixin(GoldFish.prototype, canEat, canSwim);

const goldFish  = new GoldFish();
console.log(goldFish);

```