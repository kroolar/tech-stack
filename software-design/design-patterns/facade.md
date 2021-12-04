# Facade

Structural design pattern that creates a simple interface to a more complex system.

### Problem

The **Active Record** pattern used in Ruby introduces a lot of functions that allow us to search and modify models. Instead of using the basic implementation, we can create a **Facade**, which will simplify access to the methods of this class, and in addition, it will use only what we need.

``` Ruby
class UsersFacade
  def users
    User.all
  end
 
  def active_users
    users.where(status: :active)
  end
  
  def inactive_users
    users.where(status: :inactive)
  end  
  
  def remove_inactive_users
    inactive_users.destroy_all
  end
end
```

**Pros:**
- You can isolate your code from the complexity of a subsystem

**Cons:**
-  A facade can become a god object coupled to all classes of an app.

**Sources:**
- https://refactoring.guru/design-patterns/facade
- https://refactoring.guru/design-patterns/facade/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-facade-a88e6b3949bb
