# cheatsheet-javascript
Repository for Javascript Documentation

# Index
1. Functions
2. Iterators
3. Modules
   a. Node
   b. ES6 Named Export Syntax


## Functions
To define a function using function expressions:<br>
![expression](https://github.com/user-attachments/assets/abb7c0ae-0492-447b-b173-4dd66dc8cb9a)
<br>
To define a function using arrow function notation:<br>
![arrow_notation](https://github.com/user-attachments/assets/c458794f-bd9d-44f5-9d44-eb5b6daf56f3)
<br>
Function definition can be made concise using concise arrow notation:<br>
![return](https://github.com/user-attachments/assets/e00ef0cc-4673-4872-8689-d166044de1bf)
<br>


## Iterators
<a href="https://www.codecademy.com/resources/docs/javascript/arrays/forEach" target="_blank">forEach()</a> is used to execute the same code on every element in an array but does not change the array and returns undefined.<br>
![iterator anatomy](https://github.com/user-attachments/assets/05de0dae-b4a7-498a-ac33-ecde888c7d43)
  
<a href="https://www.codecademy.com/resources/docs/javascript/arrays/map" target="_blank">map()</a> executes the same code on every element in an array and returns a new array with the updated elements.<br>
![Captura de Tela 2024-07-26 às 07 26 27](https://github.com/user-attachments/assets/0c5847eb-3a53-4c52-9c05-5334097898f0)
<br>


<a href="https://www.codecademy.com/resources/docs/javascript/arrays/filter" target="_blank">filter()</a> checks every element in an array to see if it meets certain criteria and returns a new array with the elements that return truthy for the criteria.<br>
![Captura de Tela 2024-07-26 às 07 24 22](https://github.com/user-attachments/assets/eb4a86a4-162f-4ecd-bc29-ca46bd87abe9)




<a href="https://www.codecademy.com/resources/docs/javascript/arrays/findIndex" target="_blank">findIndex()</a> returns the index of the first element of an array that satisfies a condition in the callback function. It returns -1 if none of the elements in the array satisfies the condition.<br>
![Captura de Tela 2024-07-26 às 07 23 54](https://github.com/user-attachments/assets/23d22192-7941-43c4-ade2-ffd0443c3cf6)
<br>

<a href="https://www.codecademy.com/resources/docs/javascript/arrays/reduce" target="_blank">reduce()</a> iterates through an array and takes the values of the elements and returns a single value.<br>
![Captura de Tela 2024-07-26 às 07 23 19](https://github.com/user-attachments/assets/884ee06d-dae3-4499-9996-5c45305ee529)
<br>
All iterator methods take a callback function, which can be a pre-defined function, a function expression, or an arrow function.


## Modules

Implementations of Modules in JavaScript: Node.js vs ES6

The Node runtime environment and the module.exports and require() syntax.
The browser’s runtime environment and the ES6 import/export syntax.

### Implementing Modules in Node

o create a module, you simply have to create a new file where the functions can be declared. Then, to make these functions available to other files, add them as properties to the built-in module.exports object:

```javascript
/* converters.js */
function celsiusToFahrenheit(celsius) {
  return celsius * (9/5) + 32;
}

module.exports.celsiusToFahrenheit = celsiusToFahrenheit;

module.exports.fahrenheitToCelsius = function(fahrenheit) {
  return (fahrenheit - 32) * (5/9);
};
```

The require() function accepts a string as an argument. That string provides the file path to the module you would like to import.


```javascript
/* water-limits.js */
const converters = require('./converters.js');

const freezingPointC = 0;
const boilingPointC = 100;

const freezingPointF = converters.celsiusToFahrenheit(freezingPointC);
const boilingPointF = converters.celsiusToFahrenheit(boilingPointC);

console.log(`The freezing point of water in Fahrenheit is ${freezingPointF}`);
console.log(`The boiling point of water in Fahrenheit is ${boilingPointF}`);
```


### ES6 Named Export Syntax

the functions you wish to reuse can be exported using the named export syntax below:

```javascript
export { resourceToExportA, resourceToExportB, ...}
```

Using this syntax, the name of each exported resource is listed between curly braces and separated by commas. Below, you can see how this is implemented in the new module file dom-functions.js:

```javascript
/* dom-functions.js */
const toggleHiddenElement = (domElement) => {
    if (domElement.style.display === 'none') {
      domElement.style.display = 'block';
    } else {
      domElement.style.display = 'none';
    }
}

const changeToFunkyColor = (domElement) => {
  const r = Math.random() * 255;
  const g = Math.random() * 255;
  const b = Math.random() * 255;
        
  domElement.style.background = `rgb(${r}, ${g}, ${b})`;
}

export { toggleHiddenElement, changeToFunkyColor };
```
In addition to the syntax above, in which all named exports are listed together, individual values may be exported as named exports by simply placing the export keyword in front of the variable’s declaration. Here is the same example using this syntax:

```javascript
/* dom-functions.js */
export const toggleHiddenElement = (domElement) => {
  // logic omitted...
}

export const changeToFunkyColor = (domElement) => {
  // logic omitted...
}
```

ES6 Import Syntax

The ES6 syntax for importing named resources from modules is similar to the export syntax:

```javascript
import { exportedResourceA, exportedResourceB } from '/path/to/module.js';
```

Let’s update the secret-messages program such that it now imports functionality from dom-functions.js. Doing so requires two important steps. First, update secret-messages.js:

```javascript
/* secret-messages.js */
import { toggleHiddenElement, changeToFunkyColor } from '../modules/dom-functions.js';

const buttonElement = document.getElementById('secret-button');
const pElement = document.getElementById('secret-p');

buttonElement.addEventListener('click', () => {
  toggleHiddenElement(pElement);
  changeToFunkyColor(buttonElement);
});
```
