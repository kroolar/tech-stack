# Mediator

A behavioral design pattern that restricts direct communication between objects and forces them to connect through a mediator.

### Problem

In our house, we can control the light using both app and standard switches. However, we do not want any of these solutions to be able to directly control the light because it could lead to incorrect behavior. Instead, the data will first be sent to a mediator who will be responsible for resolving these requests.

### Solution

``` Ruby

class Mediator
  def notify(_sender, _event)
    raise NotImplementedError
  end
end

class SwitchAppMediator < Mediator
  def initialize(switch, app)
    @switch = switch
    @app = app
    @switch.mediator = self
    @switch.app = self
  end
  
  def notify(_sender, event)
    if event == 'Turn On'
      # Turn on the light
    else if event == 'Turn Off'
      # Turn off the light
    else if event == 'Click'
      # Check if it is already turned on and switch state
    end
  end
end

class BaseComponent
  attr_accessor :mediator
  
  def initialize(mediator = nil)
    @mediator = mediator
  end
end

class Switch < BaseComponent
  def turn_on
    @mediator.notify(self, 'Turn On')
  end
  
  def turn_off
    @mediator.notify(self, 'Turn Off')
  end
end

switch = Switch.new
app = App.new

SwitchApp.new(switch, app)

switch.turn_on
app.click
```

**Pros:**
- You can extract the communications between various components into a single place, making it easier to comprehend and maintain (SRP)
- You can introduce new mediators without having to change the actual components (OCP)
- You can reduce coupling between various components of a program
- You can reuse individual components more easily

**Cons:**
- Over time a mediator can evolve into a God object

**Sources:**
- https://refactoring.guru/design-patterns/mediator
- https://refactoring.guru/design-patterns/mediator/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-mediator-169e77710e37
