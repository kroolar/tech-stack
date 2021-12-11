# Factory Method

A creational design pattern that creates an interface for creating objects in a base class and then replaces it depending on the type of subclass. It is a creational equivalent of **Template Method**.

### Problem

Each drink in our bar consists of two parts: alcohol and some addition. Using the Factory Method pattern, we can provide a base class that specyfi common interface for creating drinks and then we can override base methods in subclasses.

### Solution

``` Ruby
class Drink
  def create
    alcohol
    addition
  end
  
  def alcohol
    raise NoMethodError
  end
  
  def addition
    raise NoMethodError
  end
end

class WhiskyDrink < Drink
  def alcohol
    Whisky.new
  end
  
  def addition
    Ice.new
  end
end

class GinDrink < Drink
  def alcohol
    Gin.new
  end
  
  def addition
    Tonic.new
  end
end
```

**Pros:**
- You avoid tight coupling between the creator and the concrete products
- You can move the product creation code into one place in the program, making the code easier to support (SRP)
- You can introduce new types of products into the program without breaking existing client code (OCP)

**Cons:**
- The code may become more complicated since you need to introduce a lot of new subclasses to implement the pattern. The best case scenario is when you’re introducing the pattern into an existing hierarchy of creator classes

**Sources:**
- https://refactoring.guru/design-patterns/factory-method
- https://refactoring.guru/design-patterns/factory-method/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-factory-method-e4e4cd995254
