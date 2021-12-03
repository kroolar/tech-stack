# Command

### Problem
### Solution

**Pros:**
- You can decouple classes that invoke operations from classes that perform these operations (SRP)
- You can introduce new commands into the app without breaking existing client code (OCP)
- You can implement undo/redo
- You can implement deferred execution of operations
- You can assemble a set of simple commands into a complex one

**Cons:**
- The code may become more complicated since you’re introducing a whole new layer between senders and receivers

**Sources:**
- https://refactoring.guru/design-patterns/command
- https://refactoring.guru/design-patterns/command/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/command.md
- https://medium.com/@dljerome/design-patterns-in-ruby-command-802b785d1bbd
