# Mediator

### Problem
### Solution

**Pros:**
- You can extract the communications between various components into a single place, making it easier to comprehend and maintain (SRP)
- You can introduce new mediators without having to change the actual components (OCP)
- You can reduce coupling between various components of a program
- You can reuse individual components more easily

**Cons:**
- Over time a mediator can evolve into a God object

**Sources:**
- https://refactoring.guru/design-patterns/mediator
- https://refactoring.guru/design-patterns/mediator/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-mediator-169e77710e37
