# Prototype

Creational design pattern that allow you create copy of existing object.

### Problem

There is a system in which its users can report bugs or requests for new features via tickets. If the same problem occurs again, users want to be able to create a new copy of the closed ticket. 

``` Ruby
class Ticket
  attr_reader :description, :title, :type
  
  def initialize(description:, title:, type:)
    @description = description
    @title = title
    @type = type
  end

  def clone
    Bilet.new(
      description: description,
      title: title,
      type: 'asd'
    )
  end
end
```

However, it should be remembered that in Ruby the Prototype pattern is implemented in the standard library, so when creating the clone method, we overwrite the existing one. In some cases, overriding this method can be useful because the default method only makes a shallow copy of the object.

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
