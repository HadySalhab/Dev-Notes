# Design Patterns And Principles

`what’s the one thing you can always count on in software development?`
_CHANGE_

The Goal of design patterns, principles is to handle any future change in the softawre development

- Good OO designs are
  reusable, extensible and
  maintainable.

- Remember, knowing
  concepts like abstraction,
  inheritance, and polymorphism do
  not make you a good object oriented
  designer. A design guru thinks about
  how to create flexible designs that
  are maintainable and that can
  cope with change.

## Principles

- Program to an interface (supertype) and not to an implementation.
- identify the aspects that vary and separate them from what stays the same.
- Unit should be open for extension but closed for modification.
- favor composition over inheritence.
- Depend upon abstractions. Do not
  depend upon concrete classes. (Dependency inversion principle). It suggests that our
  high-level components should not depend on our low-level
  components; rather, they should both depend on abstractions.
- Strive for loosely coupled designs
  between objects that interact.

## tips

- `new` is instantiating a concrete class, so that's definetly and implementation, not an interface.
- coding to an interface, your code will work with any new classes implementing that interface through polymorphism.
- object composition allows us to change behavior dynamically at runtime
- The following guidelines can help you avoid OO designs that violate
  the Dependency Inversion Principle:

  - No variable should hold a reference to a concrete class.
  - No class should derive from a concrete class.
  - No method should override an implemented method of
    any of its base classes.

- HAS-A can be better than IS-A
- Program to an abstraction, **let your unit not know about the object in it**.

  ```java
  /*we dont know anything about the object returned to the animal, we only know that it makes sound*/
  Animal animal = getAnimal();
  animal.makeSound();
  ```

- Observer Design Patter, You can push or pull data from
  the Observable when using
  the pattern (pull is considered
  more “correct”).

## Design Patterns

### Factory

- Factories: Handle the details of object creation.
- `Simple Factory` isn’t actually a Design Pattern; it’s more of a programming idiom.
- `Factory Method`: defines an interface
  for creating an object, but lets subclasses decide which
  class to instantiate. Factory Method lets a class defer
  instantiation to subclasses.
  - useful when we do not know in advance which class we may need to instantiate and also to allow new classes to be added to the system and handle their creation without affecting client code
  - we let subclasses decide which object to instantiate by overriding the factory method.
  - we end up with a concrete creator per object type.
  - use it when you want to delegate object instantiation to subclasses.
  - This pattern has a parallel class hierarchies, Creator And Product have the same hierarchies. (Each Product has its Creator).
  - **Factory Method is not the only technique for adhering to the
    Dependency Inversion Principle, but it is one of the more powerful ones.**

### Strategy Pattern

- defines a family of algorithms,
  encapsulates each one, and makes them interchangeable.
  Strategy lets the algorithm vary independently from
  clients that use it.

### The Observer Pattern (push/pull)

- defines a one-to-many
  dependency between objects so that when one
  object changes state, all of its dependents are
  notified and updated automatically.
