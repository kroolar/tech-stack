# Chain of Responsibility

### Problem
### Solution

**Pros:**
- You can control the order of request handling
- You can decouple classes that invoke operations from classes that perform operations (SRP)
- You can introduce new handlers into the app without breaking the existing client code (OCP)

**Cons:**
- Some requests may end up unhandled

**Sources:**
- https://refactoring.guru/design-patterns/chain-of-responsibility
- https://refactoring.guru/design-patterns/chain-of-responsibility/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-chain-of-responsibility-2868e40fe8c9
