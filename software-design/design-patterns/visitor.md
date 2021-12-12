# Visitor

Behavioral design pattern that allows you to define new operations without changing the classes on which it works. In Ruby it is practically not used because most of its functionality can be replaced with a simple block.

### Problem

We create two classes, **Meal**, which contains some **price** and class **Order**, which stores some **Meals** and shows the total price of the order. We want to add new functionalities, i.e. special discounts that reduce the price of products by half, but we do not want to do it inside the class.

``` Ruby
class Meal
  attr_reader :price
  
  def initialize(price)
    @price = price
  end
end

class Order
  def initialize
    @meals = []
  end
  
  def add_meal(meal)
    @meals << meal
  end
end
```

First, we need to create a common **Visitable** module with the **accept** method.

### Solution
``` Ruby
module Visitable
  def accept(visitor)
    visitor.visit(self)
  end
end
```

Then we have to attach it from both classes and override the accept method in the **Order** class.

``` Ruby
class Meal
  include Visitable
  attr_reader :price

  def initialize(price)
    @price = price
  end
end

class Order
  include Visitable

  def initialize
    @meals = []
  end
  def add_meal(meal)
    @meals << meal
  end
  
  def total
    @meals.sum(&:price)
  end

  def accept(visitor)
    @meals.each do |meal|
      meal.accept(visitor)
    end
  end
end
```

Finally, we create a common interface for new visitors, and then inheriting from it, we can implement a specific **Visitor** who will be responsible for reducing the prices by half.

``` Ruby
class Visitor
  def visit(object)
    raise NoMethodError
  end
end

class SpecialOfferVisitor < Visitor
  def visit(object)
    object.price /= 2
  end
end

pizza = Meal.new(40)
coke = Meal.new(6)
order = Order.new
order.add_meal(pizza)
order.add_meal(coke)
order.total # => 46 

order.accept(SpecialOfferVisitor.new)
order.total # => 23
```

**Pros:**
- You can introduce a new behavior that can work with objects of different classes without changing these classes (OCP)
- You can move multiple versions of the same behavior into the same class (SRP)
- A visitor object can accumulate some useful information while working with various objects. This might be handy when you want to traverse some complex object structure, such as an object tree, and apply the visitor to each object of this structure

**Cons:**
- You need to update all visitors each time a class gets added to or removed from the element hierarchy
- Visitors might lack the necessary access to the private fields and methods of the elements that they’re supposed to work with

**Sources:**
- https://refactoring.guru/design-patterns/visitor
- https://refactoring.guru/design-patterns/visitor/ruby/example
- https://medium.com/kkempin/visitor-design-pattern-in-ruby-bc07395c4abc
