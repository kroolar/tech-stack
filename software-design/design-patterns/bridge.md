# Bridge

It separates the abstractions of its implementation, so you can modify these two elements independently.

### Problem

We have a **Users** class that allows you to retrieve data from various resources. When adding new methods, we will have to include all external resources from which we will retrieve data. At the same time, when adding another integration, we will have to modify everything.

``` Ruby
class Users
  def all(from)
    if from == 'CRM'
      # Get Users from CRM
    else
      # Get Users from application DB
    end
  end
end
```

### Solution

The Bridge pattern allows you to separate the abstraction from the implementation, which will allow you to develop both of these parts separately.

``` Ruby
class User
  def initialize(implementation)
    @implementation = implementation
  end

  def all
    @implementation.all
  end
end

class AppUsers
  def all
    # Get application Users
  end
end

class CRMUsers
  def all
    # Get users from CRM
  end
end

crm_user = User.new(CRMUsers.new)
crm_user.all # => Get Users from CRM

app_users = User.new(AppUsers.new)
app_users.all # => Get Users from DB
```

**Pros:**
- You can create platform-independent classes and apps
- The client code works with high-level abstractions. It isn’t exposed to the platform details
- You can introduce new abstractions and implementations independently from each other (OCP)
- You can focus on high-level logic in the abstraction and on platform details in the implementation (SRP)

**Cons:**
- You might make the code more complicated by applying the pattern to a highly cohesive class

**Sources:**
- https://refactoring.guru/design-patterns/bridge
- https://refactoring.guru/design-patterns/bridge/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-bridge-7aebb1b7bbc6
