# State

Each **Order** that is placed at the restaurant goes through 4 states. Depending on the condition, the customer can do several things such as pay for, pick up or rate the order. Some actions can be available in many states some only on specific one, so if we want to implement it, we would have to take into account each state in each action, which would spoil the readability of the code and make it difficult to add new states and actions in the future.

### Problem
``` Ruby
class Order
  attr_accessor :state

  def initialize
    @state = 'new'
  end
  
  def next_state
    # A lot of if-else here
  end
  
  def rate
    # A lot of if-else here
  end
  
  def pay
    # A lot of if-else here
  end
  
  def take
    # A lot of if-else here
  end
end
```

Instead, we can use the **State** pattern. First, we need to create a common interface for each state.

``` Ruby
class Order
  attr_reader :state

  def initialize
    @state = NewState.new
  end
end

class State
  def initialize(order)
    @order = order
  end

  def next_state
    raise_error
  end
  
  def rate
    raise_error
  end
  
  def pay
    raise_error
  end
  
  def take
    raise_error
  end
  
  private
  
  def raise_error
    raise 'You cannot use this method on this state'
  end
end
```

With a common parent, we can begin to build subclasses based on individual states. At this point, we want to implement only those methods that should be executed in a given state. Otherwise, an error will be raised.

``` Ruby
class NewState < State
  def next_state
    @order.state = InProgressState
  end
  
  def pay
    # Do something
  end
end

class InProgressState < State
  def next_state
    @order.state = ReadyState
  end
end

class Ready < State
  def next_state
    @order.state = ReceivedState
  end

  def take
    # Do something
  end
end

class Received < State
  def rate
    # Do something
  end
end
```

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
