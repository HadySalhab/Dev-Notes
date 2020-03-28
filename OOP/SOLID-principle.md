# SOLID principle

- Single Responsibility Principle
- Open Closed Principle
- Liskov Substitution Principle
- Interface Segragation Principle
- Dependency Inversion Principle

## Single Responsibility Principle

- The claim that `every Class should contain only one responsibility`, is correct but not practical, because the responsibility of a class is hard to be negogiated among the developers.
- A unit/class should have only _one reason_ to change, based on the reason that you have right now.We deal with future issues, in the future.
- Extract functionalities into standalone classes.
- Break features into smaller classes for easier reuse.
- In some cases, even if you can't predict how specific functionality will change in the future or whethere it will be changed at all, it is still benificial to break it into standalone classes, to allow it to be reused in another places in your system.
- Remember the Lego Bricks analogy.The smaller the component, the better.
- The Most important principle in OO design!!

## Open For Extension, Close For Modification

- Depend on stable abstractions and modify system's behavior by providing different realizations
- Is the principle that governs the usage of polymorphism.
- Strategy Design Pattern And Factory Design Pattern, obey the OCP.
- Factory design pattern, provides to our client, different realization for our abstraction @Runtime.
- strategy design patter, consist of multiple realization for our abstraction

## Liskov substitution principle

- if S is a subtype of T, then objects of type T should be replaceable with objects of type S without altering any of the desirable properties of the program
- Subtype: subclass or realization which can be substituted for the type it extends or implements.

### Rules

- Contravariance of arguments:
- Covariance of Results
- Exception Rule
- Pre-condition Rule
- Post-condition Rule
- Invariant rule
- Constraint Rule

## Interface Segregation Principle.

- helps restrict what clients can do with their services
- communicate what clients do with their services
- communicate what clients don't do with their services
