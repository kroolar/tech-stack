# Visitor

### Problem
### Solution

**Pros:**
- You can introduce a new behavior that can work with objects of different classes without changing these classes (OCP)
- You can move multiple versions of the same behavior into the same class (SRP)
- A visitor object can accumulate some useful information while working with various objects. This might be handy when you want to traverse some complex object structure, such as an object tree, and apply the visitor to each object of this structure

**Cons:**
- You need to update all visitors each time a class gets added to or removed from the element hierarchy
- Visitors might lack the necessary access to the private fields and methods of the elements that they’re supposed to work with

**Sources:**
- https://refactoring.guru/design-patterns/visitor
- https://refactoring.guru/design-patterns/visitor/ruby/example
