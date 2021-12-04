# Command

Behavioral pattern that converts certain operations into objects. They also often provide a method that allows you to reverse this operation.

### Problem

The application has a GUI in which you can create a new user with a **Button**.

``` Ruby
class Button
  def on_press
    User.new
  end
end
```

As the application develops, a button has been added that is responsible for removing a user, and then the **Button** class has been broken into two smaller subclasses.

``` Ruby
class CreateButton < Button
  def on_press
    User.new
  end
end

class RemoveButton < Button
  def initialize(user)
    @user = user
  end

  def on_press
    @user.destroy!
  end
end
```

At the next stage, several new classes were added, i.e. Client, Employee, Admin, etc. This means that each button would have to be broken into even smaller pieces, e.g. ClientSaveButton, AdminSaveButton etc. Using the **Command** pattern, we can export the command responsible for saving and the delete, restore the default **Button** class and pass it the command to execute.

``` Ruby
class SaveCommand
  def execute(object)
    object.new
  end
end

class RemoveCommand
  def execute(object)
    object.destroy!
  end
end

class Button
  def initialize(command, object)
    @command = command
    @object = object
  end
  
  def on_press
    @command.execute(@object)
  end
end
```

The Command pattern is often used in cases where you need a method that revert main command execution.

``` Ruby
class Command
  def initialize(context)
    @context = context
  end

  def execute
    @context.create
  end
  
  def unexecute
    @context.destroy
  end
end
```

### Solution

**Pros:**
- You can decouple classes that invoke operations from classes that perform these operations (SRP)
- You can introduce new commands into the app without breaking existing client code (OCP)
- You can implement undo/redo
- You can implement deferred execution of operations
- You can assemble a set of simple commands into a complex one

**Cons:**
- The code may become more complicated since you’re introducing a whole new layer between senders and receivers

**Sources:**
- https://refactoring.guru/design-patterns/command
- https://refactoring.guru/design-patterns/command/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/command.md
- https://medium.com/@dljerome/design-patterns-in-ruby-command-802b785d1bbd
