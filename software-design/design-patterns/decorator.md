# Decorator

Description

### Problem

### Solution

**Pros:**
- You can extend an object’s behavior without making a new subclass
- You can add or remove responsibilities from an object at runtime
- You can combine several behaviors by wrapping an object into multiple decorators
- You can divide a monolithic class that implements many possible variants of behavior into several smaller classes (SRP)

**Cons:**
- It’s hard to remove a specific wrapper from the wrappers stack
- It’s hard to implement a decorator in such a way that its behavior doesn’t depend on the order in the decorators stack
- The initial configuration code of layers might look pretty ugly

**Sources:**
- https://refactoring.guru/design-patterns/decorator
- https://refactoring.guru/design-patterns/decorator/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/decorator.md
- https://medium.com/@dljerome/design-patterns-in-ruby-decorator-b7f2da4153b0
