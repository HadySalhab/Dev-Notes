# Creating Collections in kotlin

```kotlin
val set = hashSetOf(1, 7, 53)

val list = arrayListOf(1, 7, 53)

val map = hashMapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```

Kotlin doesn’t have its own set of collection classes.Kotlin uses the standard Java collection classes.

Even though Kotlin’s collections are exactly the same classes as Java collections,
you can do much more with them in Kotlin

```kotlin
val strings = listOf("first", "second", "fourteenth")
println(strings.last()) //fourteenth

val numbers = setOf(1, 14, 2)
println(numbers.max()) //14
```

we can print all the element of a list

```kotlin
val list = arrayListOf("10", "11", "1001")
println(list) //[10, 11, 1001]
```

---

## Making functions easier to call

```kotlin
val list = listOf(1, 2, 3)
println(list) //[1, 2, 3]

fun <T> joinToString(
collection: Collection<T>,
separator: String,
prefix: String,
postfix: String
): String {
val result = StringBuilder(prefix)
for ((index, element) in collection.withIndex()) {
if (index > 0) result.append(separator)
result.append(element)
}
result.append(postfix)
return result.toString()
}

```

## Named arguments

```kolin
joinToString(collection, separator = " ", prefix = " ", postfix = ".")
```

---

## Default parameter values (alternative of method overloading in java)

```kotlin
//decleration
fun <T> joinToString(
collection: Collection<T>,
separator: String = ", ",
prefix: String = "",
postfix: String = ""
): String


//invoking
>>> joinToString(list, ", ", "", "") //1, 2, 3
>>> joinToString(list) //1, 2, 3
>>> joinToString(list, "; ") //1; 2; 3
```

### Java - kotlin

> Given that Java doesn’t have the concept of default parameter values, you have to
> specify all the parameter values explicitly when you call a Kotlin function with default
> parameter values from Java. If you frequently need to call a function from Java and
> want to make it easier to use for Java callers, you can annotate it with @Jvm-
> Overloads. This instructs the compiler to generate Java overloaded methods, omitting
> each of the parameters one by one, starting from the last one.

For example, if you annotate joinToString with @JvmOverloads, the following
overloads are generated:

```java
/* Java */
String joinToString(Collection<T> collection, String separator,
String prefix, String postfix);
String joinToString(Collection<T> collection, String separator,
String prefix);
String joinToString(Collection<T> collection, String separator);
String joinToString(Collection<T> collection);
```

---

## top-level functions and properties

In Kotlin, functions could be standAlone and not belong to any class. They can be placed directly at the top level of a source file.

Behind the scene, the compiler will generate a class with the same name of the file containing the function, and all top-level functions in this file are compiled to static methods of that class.

> To change the name of the generated class that contains Kotlin top-level functions,
> you add a @JvmName annotation to the file. Place it at the beginning of the file, before
> the package name:

```kotlin
@file:JvmName("StringFunctions")
package strings
fun joinToString(...): String { ... }
```

```java
/* Java */
import strings.StringFunctions;
StringFunctions.joinToString(list, ", ", "", "");
```

---

## TOP-LEVEL PROPERTIES (Stand Alone functions)

Just like functions, properties can be placed at the top level of a file.

The value of such a property will be stored in a static field.

_By default, top-level properties, just like any other properties, are exposed to Java
code as accessor methods (a getter for a val property and a getter/setter pair for a
var property). If you want to expose a constant to Java code as a public static
final field, to make its use more natural, you can mark it with the const modifier
(this is allowed for properties of primitive types, as well as String):_

```kotlin
//top level property - constant
const val UNIX_LINE_SEPARATOR = "\n"
```

```java
/* Java */
public static final String UNIX_LINE_SEPARATOR = "\n";
```

---

## Extension functions and properties (Adding methods to third party classes)

_extension function_ is a simple thing: it’s a function that can be
called as a member of a class but is defined outside of it.

```kotlin
package strings
fun String.lastChar(): Char = this.get(this.length - 1)
//String is the receiver type
//this is the receiver object
/*
The receiver type is the type on which the extension is
defined, and the receiver object is the instance of that type.*/
```

```kotlin
/*kotlin invoke*/
println("Kotlin".lastChar()) //kotlin is the receiver object
```

```java
/*Calling extension function from Java*/
//Assume lastChar() is defined in StringUtil.kt
System.out.println(StringUtilKt.lastChar("kotlin"))
```

```kotlin
fun String.lastChar(): Char = get(length - 1) //omitting `this`
```

_Note that extension functions don’t allow you to break encapsulation. Unlike methods defined in the class,
extension functions don’t have access to private or protected members of the class._

---

## Imports and extension functions

When you define an extension function, it doesn’t automatically become available
across your entire project. Instead, it needs to be imported, just like any other class or
function

```kotlin
import strings.lastChar
val c = "Kotlin".lastChar()

import strings.*
val c = "Kotlin".lastChar()

//change the name of the class
import strings.lastChar as last
val c = "Kotlin".last()
```

Changing a name on import is useful when you have several functions with the same
name in different packages and you want to use them in the same file.

---

## Calling extension functions from Java

Extension function is a static method that accepts the receiver
object as its first argument.

you call the static
method and pass the receiver object instance. Just as with other top-level functions,
the name of the Java class containing the method is determined from the name of the
file where the function is declared.

Let’s say it was declared in a StringUtil.kt file:

```JAVA
/* Java */
char c = StringUtilKt.lastChar("Java");
```

---

## Utility functions as extensions

```kotlin
//decleration
fun <T> joinToString(
collection: Collection<T>,
separator: String = ", ",
prefix: String = "",
postfix: String = ""
): String

//could be written:
//extension function with default arguments
fun <T> Collection<T>.joinToString(
separator: String = ", ",
prefix: String = "",
postfix: String = ""
): String {
val result = StringBuilder(prefix)
for ((index, element) in this.withIndex())
if (index > 0) result.append(separator)
result.append(element)
}
result.append(postfix)
return result.toString()
}
```

```kotlin
val list = arrayListOf(1, 2, 3)
>>> println(list.joinToString(" ")) //1 2 3
```

Extension functions can use a more specific type as a receiver type, not only a class.

```kotlin
fun Collection<String>.join(
separator: String = ", ",
prefix: String = "",
postfix: String = ""
) = joinToString(separator, prefix, postfix)

listOf(1, 2, 8).join() //error
```

---

## No overriding for extension functions

### Overriding principle:

Method overriding in Kotlin works as usual for member functions, but you can’t override
an extension function.

Let’s say you have two classes, View and its subclass
Button, and the Button class overrides the click function from the superclass.

```kotlin
open class View {
open fun click() = println("View clicked")
}
class Button: View() {
override fun click() = println("Button clicked")
}
```

```kotlin
val view = Button()
view.click() //Button clicked
```

**It doesn’t work that way for extensions.Extension functions aren’t a part of the class; they’re declared externally to it.
Even though you can define extension functions with the same name and parameter
types for a base class and its subclass, the function that’s called depends on the
declared static type of the variable, not on the runtime type of the value stored in that
variable.**

```kotlin
fun View.showOff() = println("I'm a view!")
fun Button.showOff() = println("I'm a button!")
 val view: View = Button()
 view.showOff() //I'm a view!
```

_When you call showOff on a variable of type View, the corresponding extension is
called, even though the actual type of the value is Button._

_As you can see, overriding doesn’t apply to extension functions: Kotlin resolves them
statically._

> If the class has a member function with the same signature as an extension
> function, the member function always takes precedence. You should
> keep this in mind when extending the API of classes: if you add a member
> function with the same signature as an extension function that a client of
> your class has defined, and they then recompile their code, it will change its
> meaning and start referring to the new member function.

---

## Extension properties

As we have seen previously, all properties in kotlin have backing fields,therefore default getters and setters. However, extension properties,
even though they’re called
properties, they can’t have any state, because there’s no proper place to store it:

```kotlin
val String.lastChar: Char
get() = get(length - 1)

 println("Kotlin".lastChar) //n
```

The getter must always be defined, because
there’s no backing field and therefore no default getter implementation

```kotlin
var StringBuilder.lastChar: Char
get() = get(length - 1)
set(value: Char) {
this.setCharAt(length - 1, value)


val sb = StringBuilder("Kotlin?")
 sb.lastChar = '!'
println(sb) //Kotlin!
}
```

---

## varargs

```kotlin
fun listOf<T>(vararg values: T): List<T> { ... }
```

allows you to pass an arbitrary
number of values to a method by packing them in an array.

In Java, you pass
the array as is, whereas Kotlin requires you to explicitly unpack the array, so that every
array element becomes a separate argument to the function being called.this feature is called using a spread operator, but in practice it’s as simple as putting the
`*` character before the corresponding argument:

```kotlin
fun main(args: Array<String>) {
val list = listOf("args: ", *args) //spread operator *
println(list)
}
```

---

## infix calls and destructuring declerations

```kotlin
val map = mapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```

The word _`to`_ in this line of code isn’t a built-in construct, but rather a
method invocation of a special kind, called an _infix call._

In an infix call, the method name is placed immediately between the target object
name and the parameter, with no extra separators.

```kotlin
//both are the same
1.to("one")
1 to "one"
```

Infix calls can be used with _regular methods and extension functions_ that have **one**
required parameter. To allow a function to be called using the infix notation, you
need to mark it with the infix modifier. Here’s a simplified version of the declaration
of the to function:

```kotlin
infix fun Any.to(other: Any) = Pair(this, other) //infix `to` creates a Pair object

val (number, name) = 1 to "one" //same as val (number, name) =  Pair(1,"one") , this equal operator will destructes the pair into number and name
```

The `to` function is an extension function to _create a pair of any elements_,
which means it’s an extension to a generic receiver: you can write 1 to "one", "one"
to 1, list to list.size(), and so on.

## Destructuring declerations:

```kotlin
val (number, name) = 1 to "one" //number = 1, name = "one"
val (number,name) = Pair(1,5) // number=1 ,name = 5

for ((index, element) in collection.withIndex()) {
println("$index: $element")
}
```

---

## Working with strings and regular expressions

`String.split()`

In Java , the argument of this funtion is a _regular expression_ or short _regex_

```Java
"12.345-6.A".split(".") //will result in an empty array, because '.' is a regular expression that denotes any character.
```

In Kotlin, we have several overloaded `split()` functions and not only one (several split() with different arguments).

The _one_ that takes a
`regular expression` requires a value of `Regex type`, not `String`. That way, it is always clear whether a string passed to a method is interpreted as plain text or a regular
expression.

```kotlin
println("12.345-6.A".split("\\.|-".toRegex())) //split the string with either dot or dash
```

Kotlin uses exactly the same regular expression syntax as in Java.
in Kotlin you use
an extension function toRegex to convert a string into a regular expression.

But for such a simple case, you don’t need to use regular expressions. The other
overload of the split extension function in Kotlin takes an arbitrary number of
delimiters as plain-text strings:

`println("12.345-6.A".split(".", "-"))`

---

## Regular expressions and triple-quoted strings

_The Kotlin standard library contains
functions to get the substring
before (or after) the first (or the last) occurrence of the given delimiter_

```kotlin
  val path = "/Users/yole/kotlin-book/chapter.adoc"
val directory = path.substringBeforeLast("/") //  /Users/yole/kotlin-book
val fullName = path.substringAfterLast("/") //  chapter.adoc
val fileName = fullName.substringBeforeLast(".") //chapter
val extension = fullName.substringAfterLast(".") //adoc
```

```kotlin
//using regular expression with triple quoted string
fun parsePath(path: String) {
val regex = """(.+)/(.+)\.(.+)""".toRegex()
val matchResult = regex.matchEntire(path)
if (matchResult != null) {
val (directory, filename, extension) = matchResult.destructured
println("Dir: $directory, name: $filename, ext: $extension")
}
}
```

_triple-quoted_ String:

In such a string, **you don’t need to
escape any characters**, including the backslash, so you
can encode the dot symbol with `\.` rather than `\\.` as
you’d write in an ordinary string literal

```kotlin
val tqs = """ hello X  \n welcome to ...""" //\n will not break a line
```

---

## Multiline triple-quoted strings

```kotlin
    val mline = """ .hey world
        .my name is X
        .and triple-quoted strings are awesome
        .kotlin
.feature
    """.trimMargin(".")
```

> The multiline string contains all the characters between the triple quotes, including
> indents used to format the code. If you want a better representation of such a string,
> you can trim the indentation (in other words, the left margin). To do that, you add a
> prefix to the string content, marking the end of the margin, and then call `trim-Margin()` to delete the prefix _AND_ the preceding whitespace in each line. _This example
> uses the dot as such a prefix_

```kotlin
//result
hey world
my name is X
and triple-quoted strings are awesome
kotlin
feature
```

A path like : "//C:\\Users\\yole\\kotlin-book"

can be written like the following:

```kotlin
"""C:\Users\yole\
kotlin-book""".

//instead of :

"C:\\Users\\yole\\kotlin-book"

//no escape needed
```

---

## Local functions and extensions

```kotlin
class User(val id: Int, val name: String, val address: String)




    fun saveUser0(user: User) {
        if (user.name.isEmpty()) {
            throw IllegalArgumentException(
                "Can't save user ${user.id}: empty Name")
        }
        if (user.address.isEmpty()) {
            throw IllegalArgumentException(
                "Can't save user ${user.id}: empty Address")
        }
// Save user to the database
    }


    fun saveUser1(user: User) {
        fun validate(value: String,
                     fieldName: String) {
            if (value.isEmpty()) {
                throw IllegalArgumentException(
                    "Can't save user ${user.id}: empty $fieldName")
            }
        }
        validate(user.name, "Name")
        validate(user.address, "Address")
        // Save user to the database
    }

fun saveUser2(user: User) {
    user.validateBeforeSave()
// Save user to the database
}

fun User.validateBeforeSave() {
    fun validate(value: String, fieldName: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException(
                "Can't save user $id: empty $fieldName")
        }
    }
    validate(name, "Name")
    validate(address, "Address")
}

```
