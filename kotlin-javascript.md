# High Order Function

## kotlin

```kotlin
fun functionReceiver(name:String,functionCall:(String)->Unit){
  //invoking the function
  functionCall(name)
}

val functionCall1 = {name:String->
println(name)
} //when storing lambda in a variable, we have to specify the type of its parameter

val functionCall3 = fun(name: String) {
    println(name)
}

fun functionCall2(name: String) {
    println(name)
}

   //function call 1
    functionReceiver("hady", functionCall1)
    //function call 2
    functionReceiver("hady", ::functionCall2)
    //function call 3
    functionReceiver("hady", functionCall3)
    //function call 4
    //declaration on Call
    //this function takes a name and print it
    functionReceiver("hady") { name ->
        println(name)
    } //parameter type is infered
```

## Javascript

```javascript
//decleration
function functionReceiver(name, functionCall) {
  functionCall(name);
}

//decleration 1
const functionCall1 = function(name) {
  console.log(name);
};
//decleration 2
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
//decleration on call
//this function takes a name and print it
//passing function to a function
functionReceiver("hady", function(name) {
  console.log(name);
});

//function call 4
functionReceiver("hady", functionCall4);

//function call 5
functionReceiver("hady", name => console.log(name));
```

- Declaration: specify the parameter and use the parameter in the body
- Invokation: ivoke by passing the arguments
- It is the responsibility of the function that receives the lambda, to call/invoke the lambda

---

# For loops

```kotlin
/*kotlin*/
   val list = listOf<String>("HADY","MILED","MELINA","ELIE")
   //reminder: Declaring the function on the call, we can store it in a variable if we want
    list.forEachIndexed{index,string->
        println("index=$index, name=$string")
    }
```

```javascript
/*javascript*/
const list = ["Hady", "Melina", "Elie", "Milad"];
//declaring the callback on the call, we can use function declaration or function expression instead.
list.forEach(function(name, index) {
  console.log(`index=${index}, name=${name}`);
});
```
