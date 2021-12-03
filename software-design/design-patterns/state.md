# State

### Problem
### Solution

**Pros:**
- Organize the code related to particular states into separate classes (SRP)
- Introduce new states without changing existing state classes or the context (OCP)
- Simplify the code of the context by eliminating bulky state machine conditionals

**Cons:**
- Applying the pattern can be overkill if a state machine has only a few states or rarely changes

**Sources:**
- https://refactoring.guru/design-patterns/state
- https://refactoring.guru/design-patterns/state/ruby/example
