
Typescript is built over JS.
Benefits
- Static Typing
- Code completion
- Refactoring

Drawbacks
 - Compilation
 - Discipline in coding
 
## Type Safety

e.g 
JS - 2 + "2"
'22'
mismatch type
null +2 
undefined + 2 -> NaN

What typescript does:
- Static Checking - check code when we're writing rather than after compiling.

## Types:

Number, String, Boolean, Null, Undefined, Void, Object, Array, Tuples, Any, Never, Unknown.

## Situations

A function accepts 2 numbers 

## Syntax
## let variableName: type = value


## Configuring TypeScript Compiler

1. In terminal type tsc --init.
2. It will create tsconfig.json.
3. Open it and set 
    - "target": "ES2016" - to change ecmascript version of compiler.
    - "rootDir": "./src" - to have ts file in src folder.
    - "outDir": "./dist" - to put all compiled js file in dist folder.
    - "noEmitOnError": true - not allowing to compile if there is ts error.
4. now type tsc on terminal it will automatically compile all files from src to dist folder.


## Debugging TS Application
 
1. Enable "sourceMap": true in tsconfig
2. It will create index.js.map - how ts code maps to js code for debuggers
3. add breakpoint in code
4. now go to vs code debugger than click on create launch.json and select Nodejs.
5. add "preLaunchTask": "tsc: build - tsconfig.json"
6. then go to index.ts and launch program



# [[Fundamentals]]