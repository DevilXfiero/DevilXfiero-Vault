
# Creating an object 

## Object 
Can contain anything as key, value pair 
```js
const circle = {
    radius : 1,
    location :{
        x: 1,
        y: 1,
    },
    isVisible: true,
    draw: function() {
        console.log('draw');
    }
}
```


Objects in JS are **dynamic** in nature i.e we can add new properties and method after creation and remove existing ones.

```js
const circle = {
    radius: 1 
};

// const circle means we cannot reassign or change circle object but we can add or remove properties.

circle.color = 'yellow';
circle.draw = function() {};
circle.location = { x: 1};

const propertyName = 'location'; 
circle[propertyName] = { x: 1}; // we can use this notation when property stored inside variable and we don't know which property to access.
console.log(circle);
delete circle.color;
delete circle.draw;
console.log(circle);
```


When our object have logic we use different ways to create using Factory or Constructor Functions.

## Factory function

```js
// Factory function

function createCircle(radius) {

    return {
        radius, // equivalent to radius: radius
        draw() {
            console.log('draw');
        }
        // equivalent to
        // draw: function() {
        //     console.log('draw');
        // }
    }
}

const circle1 = createCircle(1);
console.log(circle1);

const circle2 = createCircle(2);
console.log(circle2);
```

## Constructor Functions

```js
// Consructor Function - Pascal Notation
function Circle(radius) {
    this.radius = radius;
    this.draw = function() {
        console.log('draw');
    }
}

const circle = new Circle(1);
// 1. new operator create an empty object
// 2. set this to point to this object.
// 3. Finally it will return object from the function
console.log(circle.constructor);

```


# Constructor

Every object in JS has a property called constructor that references function that was used to create that object.

```js
let x = {};
// let x = new Object();
// bulit in Constructor Function
new String(); // but we use literal '', "",``
new Boolean(); // true, false
new Number(); // 1,2,3

```

# In JS functions are objects

```js
const Circle1 = new Function('radius', `
this.radius = radius;
this.draw = function() {
    console.log('draw');
}
`
);
const circle1 = new Circle1(1);
console.log(circle1);

Circle1.call({}, 1,2); // 1,2 are parameters same as method new Circle(1)
Circle1.apply({}, [1,2,3]); // pass arguments in array
```


## Primitives and Objects

**Value Type** or **Primitives** - Number, String, Boolean, Symbol, undefined, null
**Reference Types** or **Objects** - Object, Function, Array


```js
let x = 10;
let y = x;

x = 20;
console.log("x : " + x + " y: " + y);
// x =20, y=10 x,y are completely independent of each other.

let x1 = {value: 10};
let y1 = x1;
x1.value = 20;
console.log("x : " + x1.value + " y: " + y1.value);
// x =20, y=20
// object is not stored in the var it stored in memory and address of that memory location stored inside variable.
// copy x and y we copy refrence.
// same happens if we paas into function 
```

## Enumerating properties in object

```js
for (let key in circle) 
  console.log(key, circle[key]);
// radius 1
for(let key of Object.keys(circle))
  console.log(key);
// radius
for(let entry of Object.entries(circle))
  console.log(entry);
// [ 'radius', 1 ]
// check if property present in object
if ('radius' in circle) console.log('yes');
```

## Cloning an Object

```js
// basic
// const another = {}
// for (let key in circle) 
//   another[key] = circle[key];

// another ways
// object.assign = copies properties and methods from one or more source object into target object.
const another = Object.assign({}, circle);
// spread operator = spread an object and putting its properties and method into another.
const another1 = { ...circle };
```

- Garbage collector automatically deallocates memory for unused variables.

## Built in Objects in JS

1. Math
2. String (different from primitive JS automatically map to string to String object)
escape character to add in strings.

**Template literals** 

```js
const msg = 
`Hi ${person} ${3+4},

Thank you for joining my mailing list.

Regards,
Devilfiero
`;
```

