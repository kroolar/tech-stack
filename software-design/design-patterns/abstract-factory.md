# Abstract Factory

Description

### Problem

### Solution

**Pros:**
- You can be sure that the products you’re getting from a factory are compatible with each other
- You avoid tight coupling between concrete products and client code
- You can extract the product creation code into one place, making the code easier to support (SRP)
- You can introduce new variants of products without breaking existing client code (OCP)

**Cons:**
- The code may become more complicated than it should be, since a lot of new interfaces and classes are introduced along with the pattern

**Sources:**
- https://refactoring.guru/design-patterns/abstract-factory
- https://refactoring.guru/design-patterns/abstract-factory/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-abstract-factory-82b74682e04e
