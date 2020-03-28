- A backing field will be generated for a property if it uses the default implementation of at least one of the accessors, or if a custom accessor references it through the field identifier.

- Builder pattern can be replaced by using constructor with named arguments and default parameters.
- Decorator pattern is now easier with kotlin delegation feature : `by` keyword

## Function declaration in kotlin

```kotlin
fun functionReceiver( name:String,functionCall:(String)->Unit){
    // functionCall.invoke(name)
    functionCall(name)
}
 fun main() {
     /*
     * Passing Function to a function
     */
    //function call 1
    functionReceiver("hady", functionCall1)
    //function call 2
    functionReceiver("hady", ::functionCall2)
    //function call 3
    functionReceiver("hady", functionCall3)
    //function call 4
    //Passing Function ,that takes a name and prints it, to a function
    functionReceiver("hady") { name ->
        println(name)
    }

    /******************************/
    //storing lambda in a varialbe
val functionCall1 = { name: String ->
    println(name)
}
fun functionCall2(name: String) {
    println(name)
}
//storing anonymous function in a variable
val functionCall3 = fun(name: String) {
    println(name)

val functionCall = ::functionCall2 //storing a function in a variable (member reference)
}

```

```kotlin
fun functionReceiver2(numb1: Int, numb2: Int, sum: (Int, Int) -> Int) {
    sum(numb1, numb2)
}
fun main() {
    //call 1
    functionReceiver2(1,2,sum1)
    //call 2
    functionReceiver2(1,2,::sum2)
    //call 3
    functionReceiver2(1,2,sum3)
    //call 4
    functionReceiver2(1,2){numb1,numb2->
        numb1+numb2
    }
}

val sum1 = {numb1:Int,numb2:Int->
    numb1 + numb2
}
fun sum2(numb1:Int,numb2:Int):Int{
    return numb1+numb2
}
val sum3 = fun(numb1:Int,numb2:Int):Int{
    return numb1+numb2
}
```

## Lambda

- “When an event happens, run this handler” or
  “Apply this operation to all elements in a data structure.”
- Instead of declaring a class and passing an instance
  of that class to a function, you can pass a function directly
- you can,
  effectively, pass a block of code directly as a function parameter.

- **It is the responsibility of the function that receives the lambda, to call/invoke the lambda and pass the necessary arguments**

## Member Reference

```kotlin
fun printName(name:String){
    println(name)
}
val print = ::printName
    print("hady") //invoking

class Person(val age:Int,val name:String,val familyName:String){
    fun greeting (){
    println("hello")
}
}
val personAge = Person::age //storing age property
val personGreeting = Person::greeting //storing greeting()
val miled = Person(30,"Miled","Salheb")
println(personAge(miled)) //30
personGreeting(miled)//same as miled.greeting()
val miledAge = miled::age
println(miledAge())

```

## Collections

- The filter function goes through a collection and selects the elements for which
  the given lambda returns true. The result is a new collection that contains only the elements from the input collection
  that satisfy the predicate,
- The map function applies the given function to each element in the collection and
  collects the results into a new collection.The result is a new collection that contains the same number of elements, but each
  element is transformed according to the given predicate

```kotlin
val persons = listOf<Person>(Person(27,"Hadi","Salhab"),Person(30,"Miled","Salhab"),Person(26,"Melina","Salhab"))
val personName = persons.map(Person::name)
val personName  = persons.map { it.name } //same as above
```
