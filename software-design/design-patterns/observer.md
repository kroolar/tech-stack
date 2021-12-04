# Observer

A behavioral design pattern that aims to create a subscription method to notify multiple objects of events in an observed object.

### Problem

Every time **Client** updates their subscription plan, we want to notify the **Finance** team.

``` Ruby
class Client
  attr_reader :name, :plan

  def initialize(name, plan, finance)
    @name = name
    @plan = plan
    @finance = finance
  end
  
  def plan=(plan)
    @plan = plan
    
    @finance.update(self)
  end
end
```

Now I also want to notify the **Support** team. We can add another team to the client's implementation, but instead we can create a functionality that will help us add and remove any subscribers without interfering with the client's implementation.

### Solution

``` Ruby
class Client
  attr_reader :name, :plan

  def initialize(name, plan)
    @name = name
    @plan = plan
    @observers = []
  end
  
  def plan=(plan)
    @plan = plan
    
    notify_observers
  end
  
  def add_observers(observer)
    @observers << observer
  end
  
  def deleted_observers(observer)
    @observers.delete(observer)
  end

  def notify_observers
    @observers.each { |observer| observer.update(self) }
  end
end

client = Client.new('Microsoft', 'standard')

finance = Finance.new
support = Support.new

client.add_observer(finance)
client.add_observer(support)

client.plan = 'gold'
```

If you want to use an **Observer** pattern in Ruby, you can use the built-in **Observable** module.

``` Ruby
class Employee
  include Observable

  attr_reader :name, :title

  def initialize(name, title, salary)
    @name = name
    @title = title
    @salary = salary
  end

  def salary=(new_salary)
    @salary = new_salary
    changed
    notify_observers(self)
  end
end
```

**Pros:**
- You can establish relations between objects at runtime
- You can introduce new subscriber classes without having to change the publisher’s code (and vice versa if there’s a publisher interface) (OCP)

**Cons:**
- Subscribers are notified in random order

**Sources:**
- https://refactoring.guru/design-patterns/observer
- https://refactoring.guru/design-patterns/observer/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/observer.md
- https://medium.com/@dljerome/design-patterns-in-ruby-observer-a6e8fe2e5c0a
