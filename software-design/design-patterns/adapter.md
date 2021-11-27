# Adapter

**Type**: Structural

**Goal**: Allow to communicate between two object with incompatible interface

### Problem
Code
Solution

Nasza firma posiada wewnętrzny produkt z którego mogą korzystać tylko pracownicy. Żeby utworzyć konto w aplikacji każdy pracownik musi posiadać firmowy email oraz stanowisko, które będzie odpowiedzialne za przyznawanie uprawnień do aplikacji. Jeden z klientów także zażyczył sobie dostęp do aplikacji, jednakże aplikacja ma tylko informacje o imieniu i nazwisku klienta. 

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

Jak widzimy interfejs klasy Client nie pasuje do klasy Authenticate. W takim przypadku możemy opakować klasę Client, klasą ClientAdapter, a następnie dopasować jej interfejs tak, żeby pasował do metody create_account. 

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
- Communication interface is separated from business logic

**Cons:**
- Increase complexity. Sometimes it’s better rebuild the class

**Sources:**
- https://refactoring.guru/design-patterns/adapter
- https://refactoring.guru/design-patterns/adapter/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/adapter.md
- https://medium.com/@dljerome/design-patterns-in-ruby-adapter-89a482c26d8c

