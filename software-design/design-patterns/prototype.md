# Prototype

Description

### Problem

### Solution

**Pros:**
- You can clone objects without coupling to their concrete classes
- You can get rid of repeated initialization code in favor of cloning pre-built prototypes
- You can produce complex objects more conveniently
- You get an alternative to inheritance when dealing with configuration presets for complex objects

**Cons:**
- Cloning complex objects that have circular references might be very tricky

**Sources:**
- https://refactoring.guru/design-patterns/prototype
- https://refactoring.guru/design-patterns/prototype/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-prototype-342cb26ea75
