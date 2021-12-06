# Bridge

Description

### Problem

``` Ruby
class View
  def title
    'Hello'
  end
  
  def body
    'Some text'
  end
  
  def footer
    '2020 Copyright'
  end
end
```

### Solution

``` Ruby
  class Languages
    def title
  end
```

**Pros:**
- You can create platform-independent classes and apps
- The client code works with high-level abstractions. It isn’t exposed to the platform details
- You can introduce new abstractions and implementations independently from each other (OCP)
- You can focus on high-level logic in the abstraction and on platform details in the implementation (SRP)

**Cons:**
- You might make the code more complicated by applying the pattern to a highly cohesive class

**Sources:**
- https://refactoring.guru/design-patterns/bridge
- https://refactoring.guru/design-patterns/bridge/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-bridge-7aebb1b7bbc6
