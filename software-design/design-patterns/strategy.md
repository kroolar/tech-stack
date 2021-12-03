# Strategy

### Problem
### Solution

**Pros:**
- You can swap algorithms used inside an object at runtime
- You can isolate the implementation details of an algorithm from the code that uses it
- You can replace inheritance with composition
- You can introduce new strategies without having to change the context (OCP)

**Cons:**
- If you only have a couple of algorithms and they rarely change, there’s no real reason to overcomplicate the program with new classes and interfaces that come along with the pattern
- Clients must be aware of the differences between strategies to be able to select a proper one
- A lot of modern programming languages have functional type support that lets you implement different versions of an algorithm inside a set of anonymous functions. Then you could use these functions exactly as you’d have used the strategy objects, but without bloating your code with extra classes and interfaces

**Sources:**
- https://refactoring.guru/design-patterns/strategy
- https://refactoring.guru/design-patterns/strategy/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/strategy.md
- https://medium.com/@dljerome/design-patterns-in-ruby-strategy-1189135d2ce7
