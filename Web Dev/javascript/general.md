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

## String

[String.slice() vs String.substring()](https://stackoverflow.com/questions/2243824/what-is-the-difference-between-string-slice-and-string-substring)

## Event

Event Delegation is very handy, we want to listen to an element where it appears after the DOM was loaded (@runtime) or when we ahve multiple child elements with the same class, like list Item.

```javascript
document.querySelector(".btn-roll").addEventListener("click", btn); //callback
document.querySelector(".btn-roll").addEventListener("click", function(e) {}); //anonymous function
```

## toggle()

```javascript
document
  .querySelector(".player-0-panel")
  .classList.toggle(
    "active"
  ); /*will add the active class if it does not exist, it will remove the active class if it already exists*/
```

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
