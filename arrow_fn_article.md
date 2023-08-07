
# Article: Arrow Functions

In this lecture, we get familiar with one of the most interesting and unique concepts of Javascript - Arrow Functions. 
Arrow functions are a compact alternative to the traditional function syntax. However, they are quite particular and we have to be wise about when and how we use them. 
Let's dive in!

___

## Syntax

The name of the function is derived from the 'fat arrow' we use in between the two sides of the function.
The left side represents the parameters and the right side is derived of the expression or statement of the function. 


<p align="center">
    <img src="./pictures/arrow_functions.PNG" style="width: 60%"/>
</p>


___


### Comparing regular functions to arrow functions 

Let's take a look at a simple arrow function: 

```javascript
//Arrow Function
  let func = (param1, param2, ..., paramN) => expression;  
```

That creates a function ```func``` that accepts parameters ```param1..paramN```, then evaluates the ```expression``` using their values and returns its result. That is a shorter form of the traditional function:


```javascript
//Regular Function
let func = function(param1, param2, ..., paramN) {
  return expression;
};
```

#### using ```const``` and ```let```

Now that we've covered some syntactic differences between regular and arrow functions, let's look at some variables.

```let``` is a block-scoped variable, which means that the variable dies when the block is done.
The variable that we declare with ```let``` can be modified, but not re-declared. We use it when we know that the value of the variable will change within its scope of operation.
This, however, is not the case with ```const```.  They are also block-scoped, but they can neither be re-declared, nor changed.

<p align="center">
    <img src="./pictures/let_greet.PNG" style="width: 60%"/>
</p>

This, however, is not the case with ```const```.  They are also block-scoped, but they can neither be re-declared, nor changed.
In the following example, we create the object ```cake_01``` using the arrow function ```addVeganCake``` and ```const```. Knowing that there will be a part of the object that always stays the same, we can define that in the ```return``` statement.


```javascript
const addVeganCake = (name) => {
  return {
    name,
    diet: "vegan",
  };
};

const cake_01 = addVeganCake('Banana Chocolate Cake');
console.log(cake_01.name);
```

___

##### Arrow functions are callable, but not constructable

If a function is constructable, it can be called with ```new```, i.e. ```new User()```. 
If a function is callable, it can be called without using ```new```.

Functions created through function declarations or expressions are both constructable and callable.

Arrow functions (and methods) are ***only callable*** while class constructors are only constructable.

If you are trying to call a non-callable function or to construct a non-constructable function, you will get a runtime error.

[You can read more on callable functions here.](https://exploringjs.com/impatient-js/ch_callables.html#arrow-functions)

___


### Parameters 

#### Single parameters 

When parsing a single parameter, neither a return statement, nor parenthesis are required, thereby making the function very short.

```javascript
let double = n => n * 2; // roughly the same as: let double = function(n) { return n * 2 }
alert( double(3) );
```

#### Multiple parameters

If we need to parse multiple parameters, we need them inside parentheses.

```javascript
let sum = (a, b) => a + b;

/* This arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```

As you can see, ```(a, b) => a + b``` is a function that accepts two arguments named a and b. Upon its execution, it evaluates the expression a + b and returns the result.


#### No parameters

If there are no parameters, parentheses will be empty (but they should always be present):

```javascript
let sayHi = () => alert("Hello!");

sayHi();
```


___

### Single-line Arrow Functions vs Multiple-line Arrow Functions

Single-line functions don't require body braces around the expression. 

```javascript
let sum = (a, b) => a + b;
alert( sum(1, 2) );
```


Multiline statements require body braces and a return statement. In this case, we've got multiple parameters, so we can see the full syntax.


```javascript
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;
  return result; // if we use curly braces, then we need an explicit "return"
};

alert( sum(1, 2) );
```

___

### Returning objects in particular

There are a few ways to return an object in an arrow function. Depending on the case, what is returned will be different, and so will it's syntax.

The first and most common way is to use longform syntax.  this lets us write our variables before the ```return``` braces.

//be the -> it's. It allows-> lets us...

```javascript
const addVeganCake = (name) => {
  return {
    name,
    diet: "vegan",
  };
};

const cake_01 = addVeganCake('Banana Chocolate Cake');
console.log(cake_01);
```


A simpler way to write this is wrapping the intended object in brackets like so:

```javascript
const addVeganCake = (name) => ({
  name,
  diet: "vegan",
  });
```

By doing this, we create an expression and therefore return an expression.

___

### Differences between Regular Functions and Arrow Functions

What are the differences? 

One of the main differences between them is the syntax. Please look at the section: "Comparing traditional functions to arrow functions" to see a visual representation of that difference.

Another main difference is naming. We can not name an arrow function, however we can store it in a variable and access it that way.
Arrow functions are always anonymous.

[Storing a function in a variable example](https://youtube.com/clip/UgkxUmjy9O1HzRdT7u6ILrAtY2RRPMq4YCDM )

Second difference is that regular functions can be **hoisted** - what does that mean? It means that the function can be declared and call it before the actual declaration. This is not possible with an arrow function, because it doesn't have a name.

The third difference is that ```this``` gets handled differently within arrow functions. With arrow functions the ```this``` keyword always represents the object that defined the arrow function initially. A detailed description of this you can find in the link below.


[#2.4 'this' behaviour in Arrow Function vs. Regular Functions in JavaScript.](https://youtu.be/ebfXbjY5nhg )

In JS arguments array in functions is a special object that can be used to get all the arguments passed to the function. 
Arrow functions do not have an arguments array, but instead they get bound to arguments of enclosing scope.

To recap, let's look at the differences listed in a table.

| Regular Function  | Arrow Function |
| ----------------- | ------------- |
| Traditional Syntax | (params) => {statements} |
| Can be named or anonymous | Always anonymous  |
| Can be hoisted  | Not possible, unless inside an object  |
| ```this``` refers to owner of fn where called | ```this``` refers to owner of outside scope |
|Args array |No access to args array|

___

### Defining 'this'

In JavaScript, ```this``` is used a bit differently than in other languages like C++ or Java. The keyword ```this``` refers to the object executing the current function. It is entirely determined by **how** a function is called, and not **where** it gets defined. 

If we could simplify the usage of ```this```, it would look something like this: 

<p align="center">
    <img src="./pictures/this_formula.png" style="width: 60%"/>
</p>

If called inside of a regular object method (and not an arrow function), ```this``` references the object that the method belongs to.

At the global level, ```this``` is equivalent to a global object called ```global``` or ```window``` in browsers.

___

### Binding a regular function 

Let's look at the following example:

```javascript

class NameField {
    constructor(name) {
        const field = document.createElement('li');
        field.textContent = name;
        const nameListHook = document.querySelector('#names');
        nameListHook.appendChild(field);
    }
}

class NameGenerator {
    constructor() {
        const btn = document.querySelector('button');
        this.names = ['Max', 'Manu', 'Anna'];
        this.currentName = 0; //'this' here refers to the constructor
        btn.addEventListener('click', this.addName); // but 'this' refers to the button object
    }
    
    addName() {
        console.log(this);
        const name = new NameField(this.names[this.currentName]);
        this.currentName++;
        if (this.currentName >= this.names.length) {
            this.currentName = 0;
        }
    }
}

const gen = new NameGenerator();
```

In this example, we see that ```this``` always points to the object that owns the object-method **where ```this``` gets called**. But how do we go about fixing this?

We can use methods like ```call()```, ```apply()```, and ```bind()``` to control what ```this``` refers to.

However, these methods are **NOT** suitable when using arrow functions!

The ```call()``` and ```apply()``` methods are interchangeable. The only way they differ is the way that they supply their arguments: ```call()``` allows passing arguments one by one, separating them with commas; while ```apply()``` uses an array. 
The ```bind()``` method allows passing an array or any number of arguments, but returns a new function.

We can use ```bind()``` in our constructor as our best bet, since we don't know when the event will be fired, but we do know the desired result.

```javascript
      btn.addEventListener ('click', this.addName.bind(this));
```

The result of ```this.addName.bind(this)``` is a special function-like “exotic object”, that is callable as a function and transparently passes the call to ```addName``` setting ```this``` back to the owner of the function, which is ```NameGenerator```.

Great job, now let's see another way of going about it.

___

#### ```this``` in arrow functions

Introducing an anonymous arrow function in place of ```this.addName.bind(this)``` will work as well. That is because arrow functions let ```this``` work in a more intuitive way - it will always refer to the owner of the outside scope of the function. The anonymous function inherits the context of ```this``` since it does not get one by default.

```javascript
    btn.addEventListener('click', () => {
        this.addName();
    });
```
___


### References

1. Defining 'this' : formula [Understanding Functions and 'this' In The World of ES2017](https://youtu.be/gvicrj31JOM)
2. 'this' in object method example [JS "this" and Function References - What is it all about?](https://youtu.be/Pv9flm-80vM)
3. [Arrow Function Basics](https://javascript.info/arrow-functions-basics)
4. [const and let variables](https://brad-bartlett.medium.com/es6-advancements-arrow-functions-and-const-let-variables-f82aa960b03d)
5. [Ways to Return an Object from an Arrow Function](https://ultimatecourses.com/blog/return-object-arrow-function)
6. [What is hoisting in ES6 and how to make it work for you](https://medium.com/swlh/hoist-me-up-scotty-8a52e3d47041)
7. ["this" keyword in an arrow function](https://www.tutorialspoint.com/how-to-access-this-keyword-inside-an-arrow-function-in-javascript)


### Author
