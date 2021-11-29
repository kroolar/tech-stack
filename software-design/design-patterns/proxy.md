# Proxy

Structural pattern that manage access to given object.

There are three types of the Proxy pattern:

- **Protection Proxy**: Manages access to the objects
- **Virtual Proxy**: Delays the creation of the object until it is necessary
- **Remote Proxy**: Handle the extra code needed to send it between the two systems 

### Problem

Only **Employee** who work in the **finance** department should be allowed to access the **CompanyAccount**. In other cases, the system should raise an error.

``` Ruby
class CompanyAccount
  attr_reader :balance

  def initialize
    @balance = 0
  end
  
  def deposit(amount)
    @balance += amount
  end
  
  def withdraw(amount)
    @balance -= amount
  end
end

class Employee
  attr_reader :name, :department
  
  def initialize(name, department)
    @name = name
    @department = department
  end
end
```

### Solution

**Proxy**, like the **Adapter**, wrap the base class, their own class. The difference between these solutions is that **Proxy** provides the same interface as the base class, dealing only with object access management.

``` Ruby
class CompanyAccountProxy
  attr_reader :employee, :context
  
  def initialize(employee)
    @context = CompanyAccount.new
    @employee = employee
  end
  
  def balance
    check_access
    
    context.balance
  end
  
  def deposit(amount)
    check_access
    
    context.deposit(amount)
  end
  
  def withdraw(amount)
    check_access
    
    context.withdraw(amount)
  end

  private
  
  def check_access
    permitted? || raise_error
  end
  
  def permitted?
    employee.department == 'Finance'
  end
  
  def raise_error
    raise 'You do not have access to this resource' 
  end
end

john = Employee.new('John', 'Developer')
jane = Employee.new('Jane', 'Developer')

account = CompanyAccountProxy.new(john)
account.deposit(100) # => You do not have access to this resource

account = CompanyAccountProxy.new(jane)
account.deposit(100) # => 100
```

**Pros:**
- It allows you to manage access to the service
- It allows you to manage the service life cycle
- You can add new adapters to existing code without breaking it (OCP)

**Cons:**
- The server response may take a long time
- The code becomes more complex

**Sources:**
- https://refactoring.guru/design-patterns/proxy
- https://refactoring.guru/design-patterns/proxy/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/proxy.md
- https://medium.com/@dljerome/design-patterns-in-ruby-proxy-48a379a3b8d3
