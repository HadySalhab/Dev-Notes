# General

```Javascript
const x = form.value; //reading a value from a form -> type = string
const x = parseFloat(form.value); //always the value from the form is a string, we have to parse it to turn it to float

isFinite(monthly) //determine whether the number supplied is finite.

 form.value = //Writing a value to a form

 //for any element other than form, to get the text we use:
 element.textContent
```

> `NaN`: Not a number: As the name implies, it is used to denote that the value of an object is not a number. There are many ways that you can generate this error, one being invalid math opertaions such as 0/0 or sqrt(-1) , parsing an empty string, any arithmetic operations on undefined variable

> `undefined`: It means that the object doesn't have any value, therefore undefined. This occurs when you create a variable and don't assign a value to it.

> `null`: It means that the object is empty and isn't pointing to any memory address.

```javascript
let a = parseInt("hello");
console.log(a); //NaN

let x;
console.log(x); //undefined
```

> **WARNING**: **To check if a number is NaN, don't use the equal operator(===), instead use the utility function isNaN(number)**: Be very careful here!

> Whenever we have an element, class, id, added after the page has loaded , we need to use `Event Delegation` to fire the event on this target. [Event Delegation](https://stackoverflow.com/questions/1687296/what-is-dom-event-delegation)

```Javascript
window.location.reload(); //reload the page


Date.now() //Return the number of milliseconds since 1970/01/01:
new Date("10-03-1993") //returns the Date object corresponding to the string date passed
new Date("10-03-1993").getTime() //returns the time in millis since 1970/01/01 to the corresponding string date passed
new Date(milliscds) //get the date for this milliseconds relative to 1970/01/01

//possible constructor
new Date()
new Date(year, month, day, hours, minutes, seconds, milliseconds)
new Date(milliseconds)
new Date(date string)

date.getUTCFullYear() //Get the year as a four digit number (yyyy)

new Date(Date.now()).getUTCFullYear() //current year
```

---

## `this` keyword

**Regular function call** the `this` keyword points at the global object (window object)

**Method Call** the `this` keyword points to the object that is calling the method

**IMPORTANT**

```javascript
const object = {
  greeting() {
    console.log(this);
  },
  greeting2: () => {
    console.log(this);
  }
};

object.greeting(); // 'this' refers to the object itself
object.greeting2(); // 'this' referes to the window object
```

## String

[String.slice() vs String.substring()](https://stackoverflow.com/questions/2243824/what-is-the-difference-between-string-slice-and-string-substring)

## Event

Event Delegation is very handy, we want to listen to an element where it appears after the DOM was loaded (@runtime) or when we ahve multiple child elements with the same class, like list Item.

```javascript
document.querySelector(".btn-roll").addEventListener("click", btn); //callback
document.querySelector(".btn-roll").addEventListener("click", function(e) {}); //anonymous function
```

# DOM Manipulation

- HTMLCollections has to be converted to array so we can loop over its element

```javascript
const lis = document.getElementsByClassName("list-item");
const lisArray = Array.from(lis);
```

- Changing style from js

```javascript
//background-color-> becomes backgroundColor, //text-align-> textAlign
element.style.color = "red";
element.style.textAlign = "center";
element.style.backgroundColor = "red";
```

- DOM objects vs querySelector

```javascript
let listItemElements = document.querySelectorAll("li"); //this is a snapshot, any change to the array will not be reflected.
listItemElements = document.getElementsByTagName; //if we add an element to it, will be reflected (live).
```

- Properties VS Attributes

```javascript
const input = document.querySelector("input");
input.value = "hello"; //will be reflected in the UI and not in the Attribute.
input.setAttribute("value", "welcome"); //will change the attribute not the ui
input.value = input.getAttribute("value"); //synchronize the attribute with the ui
input.id = "input";
input.type = "email";
input.setAttribute("type", "email");
```

- Always good practise to create premade css style classes that we can add/remove/toggle to an element from our javscript instead of changing the style from javascript manually.

Example

```css
.bg-dark {
  color: #fff;
  background: #333;
}
```

```javascript
// not a good practise
element.style.color = "#fff";
element.style.background = "#333";
//good practise
element.classList.add("bg-dark");
```

## toggle()

```javascript
document
  .querySelector(".player-0-panel")
  .classList.toggle(
    "active"
  ); /*will add the active class if it does not exist, it will remove the active class if it already exists*/
```

## ClassName , ClassList

- `classList` is very handy, Since it is a list we can `add` , `remove` and `toggle` classes without overriding the classes that an element has

## AJAX

- Asynchronous Javascript & XML
- Set of web technologies to send and receive data asynchronously
- Does not interfere with the current page.(no need to reload the page)
- JSON has replaced XML for the most Part

### Process

1. JS Call (received by AJAX ENGINE)
1. AJAX ENGINE sends an XMLHttpRequest (XHR) to the Server
1. Server returns XML/JSON response (received by AJAX ENGINE)
1. AJAX ENGINE returns an HTML Response.

## Other libraries than AJAX

- Fetch API (Part of JS framework)
- Axios
- Superagent
- jQuery
- Node HTTP

## Prototypes

- Every JS object has a `prototype property` which makes inheritance possible.
- The `prototype property` of an object is where we put `methods and properties` that we want other objects to inherit.
- The `constructor's prototype property` is NOT the prototype of the constructor itself. it's the `prototype` of ALL instances that are created throught it
- When a certain `method or property` is called, the search starts is the object itself and if it cannot be found the search moves on to the object's prototype. this continues until the method is found : `Prototype Chain`

## OO js

TWO ways to create JS objects

- Object.create();
- Function Construtor
- Classes(es6) => is just a synthatic sugar, under the hood, it works like above.

## Function Borrowing

```javascript
var john = {
  calculateAge: function(){}
    //
  }
  var mike = {
   //
  }
  mike.calculateAge() = john.calculateAge();
}
```

## Passing/Declaring Callback/Function.

```javascript
//method 1 - function expression
const anyFunction = function() {
  //
};
setTimeout(anyFunction, 3000);

//method 2 - function declaration
function anyFunction() {
  //
}
setTimeout(anyFunction, 3000);

//method 3
setTimeout(function() {
  //
}, 3000);
```

```javascript
function functionReceiver(name, functionCall) {
  functionCall(name);
}

const functionCall1 = function(name) {
  console.log(name);
};

function functionCall2(name) {
  console.log(name);
}
//decleration 4
const functionCall4 = name => console.log(name);

//function call 1
functionReceiver("hady", functionCall1);
//function call 2
functionReceiver("hady", functionCall2);
//function call 3
functionReceiver("hady", function(name) {
  console.log(name);
});

//function call 4
functionReceiver("hady", functionCall4);

//function call 5
functionReceiver("hady", name => console.log(name));
```

## Arrow Functions

```javascript
//1 param 1 line body
const arrow = name => console.log(name);
//1 param 1 return
const arrow = name => "hello";
//multi param 1 return
const arrow = (name, age) => "hello";
//multi param , multi body
const arrow = (name, age) => {
  //
};
```

## Asynchronous JS

- Event Listeners, setTimeOut..(async functions) are functions that receives callback, it is the responsibility of the browser to execute the callbacks passed, whenever required. This type of operations are asynchronous, they don't block our code for them to occur
- If we have a blocking code, when we execute async code, the browser will push these executions to the message queue. When the blocking code is finished, JS will execute all the codes inside the msg queue, one after the other
- SetTimeOut(), DOM Events, XMLhttpRequests(), LocalStorage ... are part of the WEB apis and not part of the JS engine, theses are the functions that will be added to the message queue by the browser, to be executed by JS
- _Synchronous code_ are executed line-by-line , _asynchronous code_ are executed once some operation (like timeout) are completed.
- JS is **SINGLE-THREADED** , when we have asynchronous code (like setTimeOut), JS offloads these longer-taking tasks to the browser (which uses multiple threads)
- Callbacks can lead to Callbacks Hell (Not Good for Code Readability) -> Promises is the solution
- Promise takes a function in its constructor. This function is executed right away when the promise object is created.
- Promise is an object that wraps an asynchronous code. Promises has to be produced and consumed.
- we can promisify a built in api by wraping it with a Promise and return the promise to consume it
- there's no need to promisify fetch, since it returns promise by default
- returning value from `then` block will automatically be wrapped in a promise
- When having multiple promises chain, the order of the `catch` block does matter.

```javascript
const setTimer = duration => {
  //promisifying built in API
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Done");
    }, duration);
  });
  return promise;
};
```

- Async Await , was created to make consumtion of promises easier. It has nothing to do with production of promises
- Await can only run inside an `async` block
- to cosume a promise inside of an `async` block, we use `await` else we use `then`.
- Async block,since it runs in the background, will always return a `Promise` with a resolve value being the returned value specified
- Error handling in Async block is handled using the `try/catch` block

```javascript
async function getRecipeAW() {
  return recipeDetail;
}

getRecipeAW(); //the return value is a promise with resolve value equal to recipeDetail

getRecipeAW().then(); //this is how to resolve the promise to get  the recipeDetail.
```

```javascript
//Async/Await and Promises

const posData = await getPosition();
const timerData = await setTimer(2000);
console.log(timerData);

//similar
getPosition()
  .then(posData => {
    return timerData();
  })
  .then(timerData => {
    console.log(timerData);
  });
```

## Http

- url (domain+path)
- http method (GET,POST,PUT,PATCH,DELETE)
- http Headers
- http Body (data)

We have two types of error when dealing with http request:

- Server Side Error => invalid URL, invalid Data type...404 status
- client Side Error => Network error, like timeout, no internet connection

## Array

### Remove elements

1. pop - Removes from the End of an Array.
1. shift - Removes from the beginning of an Array.
1. splice - removes from a specific Array index.
1. filter - allows you to programatically remove elements from an Array.
