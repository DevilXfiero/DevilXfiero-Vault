
## Syntactic sugar over prototypical inheritance

```js
class Circle {
    constructor(radius) {
        this.radius = radius;
        this.move = function() {} // method goes to object instance
    }
    draw() {
        console.log('draw');
    } // method goes to prototype of circle object
}

const c = new Circle(1); 
```

- Unlike functions class declaration or class expression are not hoisted.

```js
// Class Declaration
class Circle {
}
// Class Expression
const square = class {
};
```

## Static Methods
```js
class Circle {
    constructor(radius) {
        this.radius = radius;
        this.move = function() {} // method goes to object instance
    }
    // Instance Method
    draw() {
        console.log('draw');
    } 
    // Static Method - not tied to a particular circle object.
    static parse(str) {
        const radius = JSON.parse(str).radius;
        return new Circle(radius);
    }

}

// Use static method to create utility functions that are not tied to a particular object.
const circle = new Circle.parse('{"radius": 1}');
console.log(circle);
```

## This keyword

```js
'use strict'; // enable strict mode if you call method as a function this by default no longer point to global object set to undefined
const Circle = function() {
    this.draw = function() {
        console.log(this);
    };
};

let c = new Circle();
// Method Call
c.draw(); // this -> Circle obj

let draw = c.draw; // getting refrence to the method
console.log(draw); // see draw function;
// Function Call - point to global object
draw(); // window object



class Circle1 {
    draw() {
        console.log(this);
    }
} // by default body of classes executed in strict mode


c = new Circle1();
draw = c.draw; 
draw(); // so it will set to undefined this will prevent from changing global object
```


## Private Members Using Symbols

```js
const _radius  = Symbol(); // essentially a unique identifier.
// Symbol() === Symbol() -> false everytime it gives unique value
const _draw = Symbol();
class Circle {
    constructor(radius) {
        this[_radius] = radius;
    }

    [_draw]() {
        
    }
    
}

const c = new Circle(2); // show property name as unique value 
// to get these properties

const key = Object.getOwnPropertySymbols(c)[0];
console.log(c[key]);
```

## Private members using WeakMaps

```js
const _radius = new WeakMap(); // keys are weak if there are no refrences to keys they're garbage collected
const _move = new WeakMap();
class Circle {
    constructor(radius) {
        _radius.set(this, radius);
        _move.set(this, () => {
            console.log('move', this);
        }); // userd arrow function to inherit this 
    }

    draw() {
        console.log(_radius.get(this));
        _move.get(this)();
    }
}
const c = new Circle(1);
```

## Getters and Setters
```js
const _radius = new WeakMap(); // keys are weak if there are no refrences to keys they're garbage collected

class Circle {
    constructor(radius) {
        _radius.set(this, radius);
    }

    get radius() {
        return _radius.get(this);
    }

    set radius(value) {
        if(value <=0) throw new Error('invalid radius');
        _radius.set(this, value);
    }
    

}
const c = new Circle(1);
c.radius = 5;
```

## Inheritance

```js
class Shape {
    constructor(color) {
        this.color = color;
    }
    move() {
        console.log('move');
    }
}

class Circle extends Shape {
    constructor(color, radius) {
        super(color); // must be used if we create constructor inside child class
        this.radius = radius;
    }
    draw() {
        console.log('draw');
    }
}

const c = new Circle("orange", 1);
```


## Method Overriding 

JS engine by default first check method in child then parent.
```js
class Shape {
    move() {
        console.log('move');
    }
}

class Circle extends Shape {
    move() {
        super.move(); // to use super method if you want
        console.log('circle move');
    }
}

const c = new Circle("orange", 1);
```