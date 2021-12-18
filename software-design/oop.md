# Object Oriented Programming

1. [Overview](#overview)
2. [Four Pillars of OOP](#fourPillars)
3. [SOLID](#solid)
4. [Principles](#principles)

### <a name="overview">1. Overview</a>

OOP is a type of programming where programs are defined by objects and the behavior between them. Object-oriented programming introduces some new terminology:

#### Class
It is a blueprint on the basis of which objects can be created.

``` Ruby
class Car
end
```

#### Object
The object is the basic building block in object-oriented languages. In Ruby, everything is an object.

``` Ruby
car = Car.new
```

#### Method
A method is a property of an object that determines its behavior.

``` Ruby
class Car
  def drive
  end
end

car = Car.new
car.drive
```

#### Attributes
Attributes are a property of a given object that determines a specific state.

``` Ruby
class Car
  attr_reader :brand
  
  def initialize(brand)
    @brand = brand
  end
end

bmw = Car.new('BMW')
bmw.brand # => "BMW"
```

#### Instance
An instance is a definition of a given object in the context of its class. (E.g. a BMW object is an instance of class Car)

### <a name="fourPillars">2. Four Pillars</a>

#### Encapsulation
It is a process that allows certain data to be wrapped into separate entities.

In the example below, we have one App class that represents our entire application. This class has several methods related to users and employees.

``` Ruby
class App
  def create_user(user, params)
    # Do something
  end
  
  def update_employee(employee, params)
    # Do something
  end
  
  def delete_user(user)
    # Do something
  end
end
```
When referring to encapsulations, we can divide them into smaller units.

``` Ruby
class User
  def create(params)
    # Do something
  end
  
  def delete
    # Do something
  end
end

class Employee
  def update(params)
    # Do soemthing
  end
end
```

#### Abstraction

Abstraction allows you to hide details that are not important, such as implementation, and show only those that are necessary. The user does not have to have access to all parts of the code, he just needs a simple interface that he will use.

``` Ruby
class CRM
  def users
    get('/users')
  end
  
  private
  
  def access_token
    # Do something
  end
  
  def get(method)
    response = HTTParty.get(method, access_token)
    
    response.body
  end
end
```
#### Inheritance
This term refers to the ability to inherit certain features and properties from other classes. We will create the Car class and include the method responsible for starting the engine in it.

``` Ruby
class Car
  def start_engine
    puts "The engine has started"
  end
end
```

Now, however, we want to create a motorcycle class, which should also contain a method that will allow the engine to start. In addition to that, we also want to add a method that will allow us to stop the engine.

Instead of adding the same methods in two different places, we can export them to a common Vehcile class, which will be able to hold values common to all vehicles, and then use inheritance to share its methods with a child class.

``` Ruby
class Vehicle
  def start_enging
    puts "The engine has started"
  end
  
  def stop_engine
    puts "The engine has stopped"
  end
end

class Car < Vehicle; end
class Motorcycle < Vehicle; end

car = Car.new
motorcycle = Motorcycle.new

car.start_engine # => "The engine has started"
motorcycle.stop_engine # => "The engine has stopped"
```

In Ruby language, only single inheritance is available, which means that a class can only inherit from one parent. However, Ruby allows you to achieve multiple inheritance by attaching modules to a given class.

#### Polymorphism

Polymorphism means the ability to take many forms. In the context of programming, it specifies that one activity can be performed in different ways. In the example above, we have declared a method that starts the engine, and it can be used for both a motorcycle and a car.


### <a name="solid">3. SOLID</a>

#### Single Responsibility Principle (SRP)
A class should only be responsible for one thing. No There should be more than one reason to modify a class.

#### Open/Closed Principle (OCP)
Classes should be open to extensions and closed to modifications.

#### Liskov Substitution Principle (LSP)
Objects that inherit from a base class should be able to replace base class objects without changing program behavior.

#### Interface Segregation Principle (ISP)
Clients should not be able to access methods that they do not use. Several smaller interfaces are better than one big one. By managing such access, any change to the interface, instead of all clients, will only apply to those affected by the change.

#### Depedency Inversion Principle (DIP)

Higher order objects should not depend on lower order objects. In the event of changes, this allows you to make changes only on the lower layers of the application, so that the higher layers can remain unchanged.

### <a name="principles">4. Principles</a>

### Law of Demether
Sometimes known as Principle of least knowledge. Specifies that the object should talk only to its closest objects. The object should not execute the method by another object.

In Rails, we often create huge unnecessary method chains through associations. Let's take this example.

``` Ruby
class User < ApplicationRecord
  belongs_to: company
end

class Company < ApplicationRecord
  has_many :users
end
```
Company stores its name, so if we want to call the company name from the user level, we can do it this way.

``` Ruby
users.company.name
```

This is breaking the Law of Demeter. The object should not contact the methods of other objects. If we want to get a company name, we should do it this way.

``` Ruby
class User < ApplicationRecord
  belongs_to: company
  
  def company_name
    company.name
  end
end

user.company_name
```

Rails are additionally equipped with the so-called delegators that allow you to shorten this entry. The equivalent of the above example is the one below.

``` Ruby
class User < ApplicationRecord
  belongs_to: company
  
  delegate :name, to: :company
end
```

### KISS
Keep It Simple, Stupid - It determines the way of designing in such a way as to do what is as simple as possible, use simple tools without any freaks, so that the structure does not contain unnecessary elements and that even the least talented of the team can understand it.

### YAGNI
You Aren't Gonna Need It - Refers to not creating redundant code. Sometimes it may seem that an implementation makes sense and may be useful in the future, but it turns out that it does not work well, or is completely unnecessary, so you have to refactor the code or remove it completely. Therefore, this method is about putting off writing code until later.

### DRY
Don't Repeat Yourself - As the name suggests, it does not mean repeating itself. It is not only about avoiding writing redundant code but also avoiding repetitive activities that can be automated.

### Composition over Inheritance
The rule is to give preference to composition over inheritance. By using inheritance, we provide the derived class with the entire interface of the base class. In the case of compositions, we can only use what we need, thanks to which we reduce the coupling between these classes.

### Encapsulate what varies
You should isolate pieces of code that may change separately. Thanks to this, when changing something in one fragment, we do not have to change anything in the other.
