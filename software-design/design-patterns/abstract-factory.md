# Abstract Factory

A creative design pattern that allows you to create similar objects without specifying their classes. It is the equivalent of the **Strategy** pattern with regarding object creation.

### Problem

Each drink in our bar consists of two parts: alcohol and some addition. Using the **Abstract Factory** pattern, we can provide a common class that will create different but similar objects based on the factory that we pass to it.

### Solution
``` Ruby
class WhiskyFactory
  def alcohol
    Whisky.new
  end
  
  def addition
    Ice.new
  end
end

class GinFactory
  def alcohol
    Gin.new
  end
  
  def addition
    Tonic.new
  end
end

class Bartender
  def initialize(drink_factory)
    @drink_factory = drink_factory
  end

  def prepare_drink
    @drink_factory.alcohol
    @drink_factory.addition
  end
end
```

**Pros:**
- You can be sure that the products you’re getting from a factory are compatible with each other
- You avoid tight coupling between concrete products and client code
- You can extract the product creation code into one place, making the code easier to support (SRP)
- You can introduce new variants of products without breaking existing client code (OCP)

**Cons:**
- The code may become more complicated than it should be, since a lot of new interfaces and classes are introduced along with the pattern

**Sources:**
- https://refactoring.guru/design-patterns/abstract-factory
- https://refactoring.guru/design-patterns/abstract-factory/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-abstract-factory-82b74682e04e
