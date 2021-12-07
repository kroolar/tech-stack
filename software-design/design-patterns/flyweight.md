# Flyweight

A structured design pattern that allows you to reduce RAM consumption by sharing states between similar objects.

- **Flyweight**: A common object that can be used in multiple contexts. It stores common state.
- **Flyweight Factory**: Class responsible for creating and storing Flyweight objects.

### Solution
``` Ruby
# Flyweight
class Color
  attr_reader :name

  def initialize(name)
    @name = name
  end
end

# Flyweight Factory
class ColorFactory
  attr_reader :colors

  def initialize
    @colors = {}
  end
  
  def find_color(name)
    if colors.has_key?(name)
      color = colors[name]
    else
      color = Color.new(name)
      colors[name] = color
    end

    color
  end
end

# Context of Use
class Canvas
  attr_reader :color_factory

  def initialize
    @color_factory = ColorFactory.new
  end
  
  def draw(x:, y:, color:)
    color = color_factory.find_color(color)
    
    # assign coordinates...
  end
end
```

**Pros:**
- You can save lots of RAM, assuming your program has tons of similar objects

**Cons:**
- You might be trading RAM over CPU cycles when some of the context data needs to be recalculated each time somebody calls a flyweight method
- The code becomes much more complicated. New team members will always be wondering why the state of an entity was separated in such a way

**Sources:**
- https://refactoring.guru/design-patterns/flyweight
- https://refactoring.guru/design-patterns/flyweight/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-flyweight-64b4d57a6f89
