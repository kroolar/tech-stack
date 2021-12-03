# Flyweight

### Problem
### Solution

**Pros:**
- You can save lots of RAM, assuming your program has tons of similar objects

**Cons:**
- You might be trading RAM over CPU cycles when some of the context data needs to be recalculated each time somebody calls a flyweight method
- The code becomes much more complicated. New team members will always be wondering why the state of an entity was separated in such a way

**Sources:**
- https://refactoring.guru/design-patterns/flyweight
- https://refactoring.guru/design-patterns/flyweight/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-flyweight-64b4d57a6f89
