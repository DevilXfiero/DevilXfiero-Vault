React is a JS library for building dynamic interfaces.
tree -> dom 

we don't need to worry about DOM we just have to use reusable component and react take care of efficiently creating and updating DOM elements.


Components help us to write reusable, modular, and better organized code.

# Creating React App

CRA official 
Vite - faster, smaller bundle size

npm create vite@latest or vite@4.1.0  specify version

go to folder 
npm i or npm install
npm run dev - to run server


# [[React Components]]


# How React Works

When App starts react takes component that component tree  and build a JS data structure called the Virtual DOM. This Virtual Dom is different from the actual DOM it's a lightweight in memory representation of component tree where each node represents a component and its properties.

When the state or data of a component changes react updates the corresponding node on the virtual DOM to reflect new state. Then it compares current version with previous version to identify the nodes that should be updated it will then update those nodes in actual DOM.
Updating DOM is done by companion library called **react-dom**.


# [[Forms]]
# [[Connecting to Backend]]

# Intermediate Topics

# [[ React Query]]
# [[Global State Management]]

# [[Routing]]


## Cross-Origin Resource Sharing (CORS)


Both backend and frontend running on same host i.e localhost but the ports are different.

We've to tell backend to allow request from different origin.



