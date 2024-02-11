
## Adding Elements 

```js
const numbers = [3,4];
// const not stop us to modify elements inside array

// Adding elements
// End
numbers.push(5,6);
// Beginning
numbers.unshift(1,2)
//Middle
numbers.splice(2, 0, 'a', 'b'); // first param - starting index, second param -number of elements to delete then elements to add
console.log(numbers);
```

## Finding Elements

```js
// Finding elements(Primitives)
const numbers  = [1, 2, 1, 4];
console.log(numbers.indexOf(1));
console.log(numbers.lastIndexOf(1));
// check if elem exist in arr
numbers.includes(1); 

numbers.indexOf(1, 2);  // second param - from index where search will begin.

// Finding refrence types
const courses = [
    { id: 1, name: 'a'},
    { id: 1, name: 'a'}
];

const course = courses.find(function(course) {
    return course.name === 'a';
}); // predicate will be passed as param return undefined if not found
courses.findIndex(function(course) {
    return course.name === 'a';
}); // return index and -1 if not present
console.log(course); 
```

## Arrow function

```js
const course = courses.find(course => course.name === 'a');
```


## Removing elements

```js
// End
const last = numbers.pop();
// Beginning
const first = numbers.shift();
// Middle
numbers.splice(2, 1);

// Emptying an array

let nums  = [1, 2, 3, 4];
let another = nums;
// Solution 1
nums = []; // but if we have multiple refrences then they will point to the prev address e.g another still points to previous arr
// Solution 2
nums.length = 0; // empty all refrences
// Solution 3 
nums.splice(0, nums.length); // noisy
// Solution 4 
while(nums.length > 0)
 nums.pop(); // noisy
```

## Combining and Slicing Arrays

```js
const first = [1, 2, 3];
const second = [4, 5, 6];
const combined = first.concat(second); // combine

const slice  = combined.slice(2, 4); // [start, end)
combined.slice(2);  // from index to end all elements
console.log(combined);
console.log(slice);
```


## Spread Operator 

```js
const combined = [...first, 'a',...second, 'b'];
console.log(combined); 
```


## Iterating array
```js
for (let number of numbers) 
  console.log(number);

numbers.forEach((number, index) => console.log(index, number)); // additional param index to get index of element
```

## Joining Arrays

```js
const numbers  = [1, 2, 1, 4];
const joined = numbers.join(','); // paas delimiter 
console.log(joined);

const message = 'This is my first message';
const parts = message.split(' '); // method of String 
console.log(parts);
```


## Sorting Arrays
```js
numbers.sort();
console.log(numbers);

numbers.reverse();
console.log(numbers);

// if we have array of objects

const courses = [
    {id: 1, name: 'Node.js'},
    {id: 2, name: 'javaScript'},
];

courses.sort((a, b) => {
    // a < b => -1
    // a > b => 1
    // a === b => 0
    const nameA = a.name.toUpperCase();
    const nameB = b.name.toUpperCase();
    // to maintain case sensitive
    if(nameA < nameB) return -1;
    if(nameA > nameB) return 1;
    return 0;
});
console.log(courses);
```

## Testing the elements of an Array

```js
const numbers = [1, 2, -1, 4];
const allPositive = numbers.every(value => value >= 0);
console.log(allPositive);

const atLeastOnePositive = numbers.some(value => value >=0);
console.log(anyPositive);
```

## Filtering  and Mapping Arrays
```js
const numbers = [1, 2, -1, 4];
const filtered = numbers.filter(value => value >=0);
console.log(filtered);

const items = filtered.map(n => '<li>' + n+ '</li>');
const objects = filtered.map(n => ({ value: n})); // if you are returing an object must put that object in paranthesis.

console.log(items);
console.log(objects);
// we can chain filter and map method.
const html = '<ul>'+ items.join('') + '</ul>';
console.log(html); 
```

## Reducing an Array

```js
let sum =0;
for (let n of numbers)
  sum += n;

const total = numbers.reduce((accumulator, currentValue) => {
    return accumulator + currentValue;
}, 0); // first argument - callBack function , second - initial value
// if we don't pass initial value first value will be set as initial value.
console.log(total);
```

