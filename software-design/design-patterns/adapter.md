# Adapter

Structural design pattern that allows communication between objects with incompatible interfaces

### Problem

The company has an internal product that only employees can access. To create an account in the application, each employee must have a company email and assigned position that will be responsible for granting access to the application. One of the clients requested access to the application, however the application only has information about the client's name and surname.

``` Ruby
class Employee
  attr_reader :email, :role
  
  def initialize(email, role)
    @email = email
    @role = role
  end
end

class Client
  attr_reader :first_name, :last_name
  
  def initalize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
end

class Authenticate
  def create_account(object)
    User.create!(
      email: object.email,
      role: object.role
    )
    
    'Account successfully created!'
  end
end

employee = Employee.new(
  email: 'john.doe@company.com',
  role: 'Developer'
)

client = Client.new('John', 'Doe')

Authenticate.new.create_account(employee) # => Account successfully created!
Authenticate.new.create_account(client) # => raise Error
```

### Solution

As we can see, the interface of the **Client** class does not match the **Authenticate** class. In this case, we can use the adapter pattern by wrapping the **Client** class with the **ClientAdapter** class, and then prepare its interface to match the **create_account** method.

``` Ruby
class ClientAdapter
  attr_reader :client

  def initialize(client)
    @client = client
  end

 def email
  "@first_name + last_name@company.com".downcase
 end
 
 def role
  'Client'
 end
end

client = Client.new(first_name: 'John', last_name: 'Doe')

client_adapter = ClientAdapter.new(client)
Authenticate.new.create_account(client_adapter) # => Account successfully created!
```

**Pros:**
- Communication interface is separated from business logic (SRP)
- You can add new adapters to existing code without breaking it (OCP)

**Cons:**
- Increase complexity. Sometimes it’s better rebuild the class

**Sources:**
- https://refactoring.guru/design-patterns/adapter
- https://refactoring.guru/design-patterns/adapter/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/adapter.md
- https://medium.com/@dljerome/design-patterns-in-ruby-adapter-89a482c26d8c
