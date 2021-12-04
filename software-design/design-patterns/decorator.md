# Decorator

Structural design pattern that allows you to add new behaviors to objects by wrapping them with decorator objects.

### Problem

Our application supports three types of users. By default, each user is a regular **User**. **Premium** users have an additional service where they can contact the support team directly, and system **Administrators** have an additional feature that allows adding roles to users.

``` Ruby
class User  
  def initialize(name)
    @name = name
  end

  def role
    'user'
  end
end
```

Using the Decorator pattern, we should implement the same interface as the original class, while each subclass should add new functionalities to it.

``` Ruby
class UserDecorator
  def initialize(user)
    @user = user
  end
  
  def name
    @user.name
  end
  
  def role
    @user.role
  end
end

class AdminUser < UserDecorator
  def role
    'admin'
  end
  
  def update_user_role(role)
    user.role = role
  end
end

class PremiumUser < UserDecorator
  def role
    'premium'
  end
  
  def send_request(text)
    # Send email to support team
  end
end
```

**Pros:**
- You can extend an object’s behavior without making a new subclass
- You can add or remove responsibilities from an object at runtime
- You can combine several behaviors by wrapping an object into multiple decorators
- You can divide a monolithic class that implements many possible variants of behavior into several smaller classes (SRP)

**Cons:**
- It’s hard to remove a specific wrapper from the wrappers stack
- It’s hard to implement a decorator in such a way that its behavior doesn’t depend on the order in the decorators stack
- The initial configuration code of layers might look pretty ugly

**Sources:**
- https://refactoring.guru/design-patterns/decorator
- https://refactoring.guru/design-patterns/decorator/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/decorator.md
- https://medium.com/@dljerome/design-patterns-in-ruby-decorator-b7f2da4153b0
