# Builder

Creational design pattern that allows create complex objects step by step.

### Problem

We want to build a **House**. Depending on the needs, we can add **Rooms** to it, we can choose whether we want a **Garage** and whether this garage has an **Automatic Gate**.

``` Ruby
class House
  attr_accessor :rooms, :garage
  
  def initialize
    @rooms = []
    @garage = false
  end
end

class Room
  attr_reader :name
  
  def initialize(name)
    @name = name
  end
end

class Garage
  attr_accessor :automatic_gate
  
  def initialize
    @automatic_gate = false
  end
end

garage = Garage.new
garage.automatic_gate = true

kitchen = Room.new('Kitchen')

house = House.new
house.garage = garage
house.rooms << kitchen
```

### Solution

As we can see above, we need to know the implementation of each class, set it appropriately, and then write to the **House** class. By implementing the **Builder** pattern, we create one common interface that focuses on creating a **House** without going into the implementation details of each class.

``` Ruby
class HouseBuilder
  attr_reader :house
  
  def initialize
    @house = house
  end
  
  def garage(has_garage = true)
    return unless has_garage

    @house.garage = Garage.new
  end
  
  def add_room(name)
    @house.rooms << Room.new(name)
  end
  
  def automatic_garage_gate(has_automatic_gate = true)
    raise "This house has no garage! " if @house.garage.nil?

    @house.garage.automatic_gate = has_automatic_gate
  end
end

builder = HouseBuilder.new

builder.garage
builder.automatic_garage_gate
builder.add_room('Kitchen')
```

**Pros:**
- You can construct objects step-by-step, defer construction steps or run steps recursively
- You can reuse the same construction code when building various representations of products
- You can isolate complex construction code from the business logic of the product (SRP)

**Cons:**
- The overall complexity of the code increases since the pattern requires creating multiple new classes

**Sources:**
- https://refactoring.guru/design-patterns/builder
- https://refactoring.guru/design-patterns/builder/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/builder.md
- https://medium.com/@dljerome/design-patterns-in-ruby-builder-6c6d172e8de8
- https://github.com/KoKumagai/design-patterns-in-Ruby/blob/master/creational/builder/builder.rb
