# Template Method

### Problem
### Solution

**Pros:**
- You can let clients override only certain parts of a large algorithm, making them less affected by changes that happen to other parts of the algorithm
- You can pull the duplicate code into a superclass

**Cons:**
- Some clients may be limited by the provided skeleton of an algorithm
- You might violate the Liskov Substitution Principle by suppressing a default step implementation via a subclass
- Template methods tend to be harder to maintain the more steps they have

**Sources:**
- https://refactoring.guru/design-patterns/template-method
- https://refactoring.guru/design-patterns/template-method/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/template_method.md
- https://medium.com/@dljerome/design-patterns-in-ruby-template-method-753443f5a1c8
