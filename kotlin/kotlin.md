# Kotlin In Action - Summary

## Kotlin, first meeting

- Statically Typed Language: The type of every expression in a program is known at compile time, and the compiler can validate that the methods and fields you’re trying to access exist on the objects you’re using
- Type Inference: the type of a variable can automatically be determined from the context, allowing you to omit the type declaration.
- Support for Nullable Types: Helps avoid null pointer exception
- Support for function types :

  - working with functions as values gives you much more power of abstraction, which lets you avoid duplication in your code. Imagine that you have two similar code fragments that implement a similar task(for example, looking for a matching element in a collection) but differ in the details (how the matching element is detected).
    **You can easily extract the common part of the logic into a function and pass the differing parts as arguments. Those arguments are themselves functions, but you can express them using a concise syntax for anonymous functions called lambda expressions.**

    - ```Kotlin
      //findPerson() contains the general logic to find a person
      //the lambda itself identifies the logic to find the specific person you need.
      fun findAlice() = findPerson { it.name == "Alice" }
      fun findBob() = findPerson { it.name == "Bob" }
      ```

  - easier testing
  - safer multithreading
  - `Function types:` allowing functions to receive other functions as params or return other functions
  - `Lambda expressions` letting you pass around blocks of code with minimum boilerplat
  - `Data classes` provide concise syntax for creating immutable value objects
  - Rich set of APIs to work with objects and collections in the functional style.

When writing code in Kotlin, you can combine both the object-oriented and functional approaches and use the tools that are most appropriate for the problem you’re solving.

---

## Kotlin philosophy

- Pragmatic : kotlin was created to address use cases encountered by many software developers
- concise : takes less time to write and, more important, less time to read
- Safe language:

  - Kotlin strives to remove the `NullPointerException` from your program.
    - ```kotlin
      val s: String? = null //can be null
      val s2: String = "" //cannot be null
      ```
  - Kotlin helps avoid `ClassCastException`

    - ```kotlin
        if (value is String)
        println(value.toUpperCase()) //since this code cannot be generated unless value is a string, kotlin provides smart-casting, which means kotlin knows at this stage that value is a string, so we can apply to value any string method
      ```

---

## Kotlin Basic

Statements and expressions

In Kotlin, `if` is an expression, not a statement. The difference between a statement
and an expression is that an expression has a value, which can be used as part of
another expression, whereas a statement is always a top-level element in its enclosing
block and doesn’t have its own value. In Java, all control structures are statements.
In Kotlin, most control structures, except for the loops (for, do, and do/
while) are expressions. The ability to combine control structures with other expressions
lets you express many common patterns concisely, as you’ll see later in the
book.
On the other hand, assignment are expressions in Java and become statements in
Kotlin. This helps avoid confusion between comparisons and assignments, which is
a common source of mistakes.

```kotlin

fun max(a: Int, b: Int): Int {
return if (a > b) a else b  //block body
}

fun max(a: Int, b: Int): Int = if (a > b) a else b //expression body

fun max(a: Int, b: Int) = if (a > b) a else b //expression body with type inference


/*
Note that omitting the return type is allowed only for functions with an expression
body. For functions with a block body that return a value, you have to specify the
return type and write the return statements explicitly*/

```

---

## Variables

```kotlin
//type inference
val question = "The Ultimate Question of Life, the Universe, and Everything"
val answer = 42

//If a variable doesn’t have an initializer, you need to specify its type explicitly:
//The compiler can’t infer the type if you give no information about the values that can
be assigned to this variable.

val answer: Int
answer = 42

```

Two types of variables in kotlin

- val: (from value)—Immutable reference. A variable declared with val can’t be
  reassigned after it’s initialized. It corresponds to a final variable in Java.
- var: (from variable)—Mutable reference. The value of such a variable can be
  changed. This declaration corresponds to a regular (non-final) Java variable.

By default, you should strive to declare all variables in Kotlin with the val keyword.
Change it to var only if necessary.

A val variable must be initialized exactly once during the execution of the block
where it’s defined. But you can initialize it with different values depending on some
condition, if the compiler can ensure that only one of the initialization statements will
be executed

```kotlin
val message: String
if (canPerformOperation()) {
message = "Success"
// ... perform the operation
}
else {
message = "Failed"
}
```

Note that, even though a val reference is itself immutable and can’t be changed, the
object that it points to may be mutable. For example, this code is perfectly valid:

```kotlin
val languages = arrayListOf("Java")
languages.add("Kotlin")
```

Even though the var keyword allows a variable to change its value, its type is fixed.
For example, this code doesn’t compile:

```kotlin
var answer = 42
answer = "no answer"
```

---

## String Template

```kotlin
fun main(args: Array<String>) {
val name = if (args.size > 0) args[0] else "Kotlin"

println("Hello, $name!") //include variable in strings

println("$name has ${name.length} characters") //we can include expressions
}

/*
* we can include any expression
*/
fun main(args: Array<String>) {
println("Hello, ${if (args.size > 0) args[0] else "someone"}!")
}
```

---

## Classes

```java
/* Java */
public class Person {
private final String name;
public Person(String name) {
this.name = name;
}
public String getName() {
return name;
}
}
```

```kotlin
/*Kotlin*/
/*Unlike java which has the default modifier by default
kotlin has public modifier by default, so we can omit it
*/
class Person(val name: String)
```

---

## Properties

Java

```java
/* Java */
public class Person {

//Field
private final String name;
public Person(String name) {
this.name = name;
}

/*
*Accessor methods
*/
public void setName(String name){
  this.name = name;
}
public String getName() {
return name;
}
}
```

In java, Combination of Fields and Accessor is often referred as Properties. In Kotlin, properties are a
first-class language feature, which entirely replaces fields and accessor methods.You
declare a property in a class the same way you declare a variable: with val and var
keywords. A property declared as val is read-only, whereas a var property is mutable
and can be changed.

Kotlin

```kotlin
/*Kotlin*/
//name and isMarried are PROPERTIES
class Person(val name:String,var isMarried:Boolean)

//name: immutable property
//isMarried : mutable property

/*
behind the scene, kotlin created 2 fields to these properties respectively to store their values, a getter for the immutable property (to get its value) and both getter and setter (to get and set the value of the mutable property)
*/
```

The above Snippet: *it’s a class with *private\* fields that is initialized
in the constructor and can be accessed through the corresponding getter.

```Kotlin
val person = Person("Harry",true)
//we are accessing the property directly, but behind the scene the getter and setter is invoked or returned and NOT the field itself

//same concept of java, but different syntax(more concise)
person.name //person.getName() <- behind the scene
person.isMarried //person.isMarried() <-behind the scene
```

---

## Custom accessors

```kotlin
class Rectangle(val height: Int, val width: Int) {
val isSquare: Boolean
get() {
return height == width //will do the calculation on the fly
//isSquare does not need a field to store its value
}
//or
get() = height == width,
}
```

The above check could have been replaced with a function

```kotlin
class Rectangle(val height: Int, val width: Int) {

fun isSquare():Boolean = heigh == width
}
```

Both snippets are the same, but a good rule of thumb is _if you describe the
characteristic (the property) of a class, you should declare it as a property._

---

## Kotlin source code layout: directories and packages

In Kotlin, you can put multiple classes in the same file and choose any name for that
file.
However, it’s still a good practice to follow Java’s directory layout and to
organize source files into directories according to the package structure. Sticking to
that structure is especially important in projects where Kotlin is mixed with Java

---

## enums and “when”

## `enums`

Keyword: `enum class`

```kotlin
enum class Color {
RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```

Enums with constants, properties and functions:

```kotlin
//properties
enum class Color(val r: Int, val g: Int, val b: Int) {
  //constants are seperated with commas
RED(255, 0, 0), ORANGE(255, 165, 0),
YELLOW(255, 255, 0), GREEN(0, 255, 0), BLUE(0, 0, 255),
INDIGO(75, 0, 130), VIOLET(238, 130, 238); //don't forget the last semicolons after the last constants


//functions
fun rgb() = (r * 256 + g) * 256 + b
}
```

Enum constants use the same constructor and property declaration syntax as you saw
earlier for regular classes. When you declare each enum constant, you _need_ to provide the property values for that constant. Don't forget the semicolons: after the last constant

---

## `when`

## `when` with enum

Like `switch` in Java

```kotlin
//when, like if ,is an expression and not a statement
//so we can use expression body instead of block body
fun getMnemonic(color: Color) =
when (color) {
Color.RED -> "Richard"
Color.ORANGE -> "Of"
Color.YELLOW -> "York"
Color.GREEN -> "Gave"
Color.BLUE -> "Battle"
Color.INDIGO -> "In"
Color.VIOLET -> "Vain"
}
```

---

## `when` Combination of values

```kotlin
//combination
//We can also combine multiple values in the same branch if you separate them with commas.
fun getWarmth(color: Color) = when(color) {
Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
Color.GREEN -> "neutral"
Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
}
```

---

## `when` with arbitary objects

In Java, `switch`
requires you to use constants (enum constants, strings, or number literals) as
branch conditions,

In Kotlin,`when` can be used with any object in kotlin:

We can use the `set` collection for which the order of items doesn’t matter; two
sets are equal if they contain the same items.

Example:

```kotlin
val set1 = setOf(1, 2, 3)
val set2 = setOf(3, 2, 1)

// setOf preserves the iteration order of elements
println(set1) // [1, 2, 3]
println(set2) // [3, 2, 1]

// but the sets with the same elements are equal no matter of order
println("set1 == set2 is ${set1 == set2}") // true
```

```kotlin
//expression body as well
fun mix(c1: Color, c2: Color) =
when (setOf(c1, c2)) {
setOf(RED, YELLOW) -> ORANGE
setOf(YELLOW, BLUE) -> GREEN
setOf(BLUE, VIOLET) -> INDIGO
else -> throw Exception("Dirty color") //when none of the cond. is met
}
```

If the sets setOf(c1, c2) and setOf(RED, YELLOW) are equal, it means either c1 is RED and c2 is YELLOW, or vice
versa.

---

## Boolean expression with `when` (without arguments)

```kotlin
fun mix(c1: Color, c2: Color) =
if((c1==RED && c2==YELLOW) || (c1==YELLOW || c2 == Red)){

}else if(...)
```

```kotlin
fun mixOptimized(c1: Color, c2: Color) =
//no arguments
when {
(c1 == RED && c2 == YELLOW) ||
(c1 == YELLOW && c2 == RED) ->
ORANGE
(c1 == YELLOW && c2 == BLUE) ||
(c1 == BLUE && c2 == YELLOW) ->
GREEN
(c1 == BLUE && c2 == VIOLET) ||
(c1 == VIOLET && c2 == BLUE) ->
INDIGO
else -> throw Exception("Dirty color")
}
```

_If 'no argument' is supplied for the `when` expression, the branch condition is any Boolean
expression_

---

## Smart Cast (Combining type checks with cast)