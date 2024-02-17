```ts
let sales: number  =  12345678;
let num = 1234; // we always don't have to annotate ts compiler detect it base on the value
let course: string = 'TypeScript';
let is_published: boolean = true;
let level; // assumes it of type any
```

# The any type

```ts
let level; // assumes it of type any which can refer any values
level = 1;
level = 'a'; // against loose feature and benefit of using ts
```

## Arrays
```ts
let numbers: number[]  = [1, 2, 3]; // or let numbers = [1, 2, 3]
let nums = []; // any type
```
## Tuples

```js
let user: [number, string] = [1, 'Mosh'];
user[0] 
user[1]
```

## Enums

```ts
enum Size {Small = 1, Medium = 2, Large = 3};
const enum CharSize {Small = 's', Medium = 'm', Large = 'l'}; // compiler generate more optimized code for const

let mySize: Size = Size.Medium;
console.log(mySize);
```

## Function 
```ts
function calculateTax(income: number, taxYear: number): number /*return type of functino eg. void, boolean etc */ {
    if (taxYear < 2022)
       return income * 1.2;
    return income * 1.3;
} // infered return value 

// to make second param optional 
function calculateTaxOneParam(income: number, taxYear = 2022 /* default value */): number /*return type of functino eg. void, boolean etc */ {
    if (taxYear < 2022)
       return income * 1.2;
    return income * 1.3;
}
```

"noUnusedParameters": true -  Raise an error when a function parameter isn't read.
"noImplicitReturns": true  - Enable error reporting for codepaths that do not explicitly return in a function.
"noUnusedLocals": true - Enable error reporting when local variables aren't read.

## Objects

```ts
let employee: {
    readonly id: number, // readonly not editable
    name: string,
    retire: (date: Date) => void
} = {
id: 1, 
name: 'Mosh',
retire: (date: Date) => {
    console.log(date);
}
};

```

