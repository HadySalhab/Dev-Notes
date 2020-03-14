# Logical Layers

In a GUI system we can have 4 abstract layers

- User Interface layer (UI)
- Application Layer
- Domain layer
- infrastructure layer

## UI layer

- Capture user interactions with UI elements and route them into the system. (But does not handle it or proccess it)
- Render system output

## Application layer

- control user flow inside the system (like navigation between screens)
- Pass system output to UI layer
- handle user interactions with UI layer
- Glue layer, integrate standalone piece of functionality from other layer

## domain layer

- Execute Business domain flows (business logic) , like add to cart, checkout in an e-commerce app

## Infrastructure layer

- General functionality, database,network,event buses.

## Presentation layer = UI layer + Application layer

- Render system output
- capture and handle user interactions with UI elements
- control user flow into the system

# Presentation Layer Architectural Pattern

> Reusable high level structure for presentation layer organization.

# MVx

- M = Model

  - state &/ business logic &/ data structures

- V = view , UI
- X
  - Business logic &/ flow control logic &/ state &/ data structures.
