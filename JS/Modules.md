
Splitting code into multiple files called modules.


- Maintainability
- Reuse
- Abstract


Before ES6 
## Module Formats

AMD - Asynchronous module definition
CommonJS - Node.js
UMD - Universal module definition
ES6 Modules - Browsers


## CommonJs Modules

circle.js
```js
// Implementation Detail
const _radius = new WeakMap();


// Public Interface - what we're exporting
class Circle {
    constructor(radius) {
      _radius.set(this, radius);
    }

    draw() {
        console.log('Circle with radius ' + _radius.get(this));
    }
}
// module.exports.Circle = Circle;
// module.exports.Shape = Shape //to export multiple from single module
module.exports = Circle;

```

index.js
```js
const Circle = require('./circle');
const c = new Circle(10);
```


## ES6 Modules

By default all private have to use export.

circle.js
```js
// Implementation Detail
const _radius = new WeakMap();
// Public Interface - what we're exporting
export class Circle {
    constructor(radius) {
      _radius.set(this, radius);
    }

    draw() {
        console.log('Circle with radius ' + _radius.get(this));
    }
}
```

index.js
```js
import {Circle} from "./circle.js";

const c = new Circle(10);
c.draw();
```

## ES6 Tooling

Transpiler(Translator + Compiler) ->  convert modern JS code to code all browser can understand e.g Babel.

Bundler -> combine all JS file to single JS file called bundle. e.g Webpack



