# Factory Method

Description

### Problem

### Solution

**Pros:**
- You avoid tight coupling between the creator and the concrete products
- You can move the product creation code into one place in the program, making the code easier to support (SRP)
- You can introduce new types of products into the program without breaking existing client code (OCP)

**Cons:**
- The code may become more complicated since you need to introduce a lot of new subclasses to implement the pattern. The best case scenario is when you’re introducing the pattern into an existing hierarchy of creator classes

**Sources:**
- https://refactoring.guru/design-patterns/factory-method
- https://refactoring.guru/design-patterns/factory-method/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-factory-method-e4e4cd995254
