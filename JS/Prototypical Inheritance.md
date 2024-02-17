
## Creating own prototypical Inheritance

```js
function Shape() {

}
Shape.prototype.duplicate = function() {
    console.log('duplicate');
}
function Circle(radius) {
    this.radius = radius;
}
Circle.prototype = Object.create(Object.prototype); // Implicit relationship
Circle.prototype = Object.create(Shape.prototype); // create object inherit from shape prototype

Circle.prototype.draw = function() {
    console.log('draw');
}

const s  = new Shape();
const c = new Circle(1);
```

## Resetting the Constructor

Whenever we reset the prototype best practice is to reset the constructor other wise it will change to new prototype set.
```js
// Circle.prototype.constructor = Circle;
// new Circle.prototype.constructor => new Circle()
Circle.prototype = Object.create(Shape.prototype); // create object inherit from shape prototype
Circle.prototype.constructor = Circle;
```

## Calling the super constructor
```js
function Shape(color) {
    this.color = color;

}
Shape.prototype.duplicate = function() {
    console.log('duplicate');
}
function Circle(radius, color) {
    Shape.call(this, color);
    this.radius = radius;
}

Circle.prototype = Object.create(Shape.prototype); 
Circle.prototype.constructor = Circle;

// if 
Circle.prototype.draw = function() {
    console.log('draw');
}
const c = new Circle(1, 'red');
```

## Intermediate Function Inheritance
```js
function Square(size) {
    this.size = size;
}
// intermediate function to set parent prototype.
function extend(Child, Parent) {
    Child.prototype = Object.create(Parent.prototype); 
    Child.prototype.constructor = Child;
}
extend(Square, Shape);
```

## Method Overriding

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
function Circle(radius, color) {
    this.radius = radius;
}
extend(Square, Shape);
Circle.prototype.duplicate = function() {
    Shape.prototype.duplicate.call(this);
    console.log('duplicate circle');
}
```

