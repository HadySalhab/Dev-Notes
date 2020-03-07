In Javascript we can insert full array into the local storage with a corresponding key:

```Javascript
let tasksLS;
  if (localStorage.getItem("key") === null) {
    tasksLS = [];
  } else {
    tasksLS = JSON.parse(localStorage.getItem("tasks"));
  }
  //do anything with the array...
  localStorage.setItem("key", JSON.stringify(tasks));


```

```Javascript
 //ClassName must include all the classes of an element
  if (e.target.className === "fa fa-remove") {
    e.target.parentElement.parentElement.remove();
  }
```

```Javascript
if (confirm("Are You Sure?")) {
   // will prompt a dialog to the user.
   //if user presses ok -> the if will proceed
    }

```

```Javascript
  document.addEventListener("DOMContentLoaded", function); //the function will fire as soon as the DOM is loaded
```
