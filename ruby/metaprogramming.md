# Metaprogramming

1. [Overview](#overview)
2. [Method Missing](#methodMissing)
3. [Send](#send)
4. [Instance Methods](#instanceMethods)
5. [Respond To](#respondTo)
6. [Instance Variables](#instanceVariables)
7. [Hierarchy](#hierarchy)
8. [Instance Eval](#instanceEval)
9. [Define Method](#defineMethod)


### <a name="overview">1. Overview</a>
Metaprogramming means creating programs that can create and modify their own code while the program is running. Ruby as a really dynamic language provides many tools to help with this.

<br>

### <a name="methodMissing">2. Method Missing</a>
One of the most popular methods used in meta-programming is **method_missing**. This method allows you to perform an operation if no matching method is found. To **method_missing** we have to pass the called method and optionally we can also pass arguments and block.

The following code shows a possible implementation of the **ActiveRecord** class, which allows multiple methods to be called even though they are not defined in the **ActiveRecord** class.

``` Ruby
class ActiveRecord
  def self.find_by(query)
    key = query.keys.first
    value = query[key]

    puts "Ruby is looking for #{to_s.pluralize} with #{key.to_s.humanize} equal #{value}"
  end

  def self.method_missing(method, *args, &block)
    super unless method.to_s.start_with?('find_by_')

    method_name = method.to_s.gsub('find_by_', '')

    find_by(method_name => args.first)
  end
end

class User < ActiveRecord; end

User.find_by(name: 'John') # => "Ruby is looking for Users with Name equal John"

User.find_by_name('John') # => "Ruby is looking for Users with Name equal John"
User.find_by_email('j.doe@mail.com') # => "Ruby is looking for Users with Email equal j.doe@mail.com"

User.where(name: 'John') # => NoMethodError: undefined method `where' for User:Class
```
<br>

### <a name="send">3. Send</a>
Method **send** allow to invoke a method based on string or symbol passed as an argument.

``` Ruby
class User
  def initialize(age:, email:, name:)
    @age = age
  end
  
  def attribute(name)
    send(name)
  end
  
  private
  
  attr_reader :age, :email, :name
end

john = User.new(
  age: 25,
  email: 'j.doe@mail.com', 
  name: 'John Doe'
)

john.age # NoMethodError: private method `age' called for #<User:0x00005636a4e10768>
john.attribute(:name) # => 'John Doe'
john.attribute('age') # => 25
```
<br>

### <a name="instanceMethods">4. Instance Methods</a>
The **instance_methods** method allows us to check the available methods of a given instance. This method returns an array of all available methods, including those inherited from other classes, so it is most often used with the argument **false**, which omits inherited methods.

``` Ruby
class Checklist
  def complete_all
    complete_first_task
    complete_second_task
 
    # and so on...
  end

  def complete_first_task
    'First task completed'
  end

  def complete_second_task
    'Second task completed'
  end

  # and so on...
end
```

In this case, we don't want to list all of the available methods, we just want to get them and then call them. Obviously removing the current method in which it is called so as not to create an infinite loop.

``` Ruby
  def complete_all
    all_methods = self.class.instance_methods(false) - [:complete_all]

    all_methods.map { |method| send(method) }
  end
```
<br>

### <a name="respondTo">5. Respond To</a>
The **respond_to?** method is often used in meta programming. It allows us to check whether a given method can be called by an object or class.

``` Ruby
class User
  def manager; end
end

john = User.new

john.respond_to?(:manager) # => true
john.respond_to?(:employeer) # => false
```
<br>

### <a name="instanceVariables">6. Instance Variables</a>
Ruby allows to check what instance variables we have with method **instance_variables**

``` Ruby
class User
  attr_reader :age, :name
  
  def initialize(age:, name:)
    @age = age
    @name = name
  end
end

john = User.new(age: 25, name: 'John Doe')
john.instance_variables # => [:@age, :@name]
```
<br>

### <a name="hierarchy">7. Hierarchy</a>
In some cases, the object should be aware of its surroundings. This is where the **class** and **superclass** methods come in handy. The first checks what class a given object is, and the second checks the parent's class.

``` Ruby
class User; end

u = User.new

u.class # => User
u.class.superclass # => Object
```

We can also check all ancestors with **ancestors** method.

``` Ruby
class User; end

User.ancestors # => [User, Object, Kernel, BasicObject]
```

We do not know what is a module and what is class, but we can easily check it.

``` Ruby
User.ancestors.map { |a| "#{a.class}: #{a}" } # => ["Class: User", "Class: Object", "Module: Kernel", "Class: BasicObject"] 
```
<br>

### <a name="instanceEval">8. Instance Eval</a>
The **instance_eval** method allows you to run code from the object you are calling it on. This method is often used to write DSL.

Example of invoke private method.

``` Ruby
class User
  private
  
  def hello
    'Hello World!
  end
end

u = User.new
u.hello_world # => NoMethodError (private method `hello' called for #<User:0x0000561ad6775eb0>)
u.instance_eval('hello') # => 'Hello World!'
```

Example of adding new method to existing code at runtime.

``` Ruby
class User; end

u = User.new
u.hello # => NoMethodError (undefined method `hello' for #<User:0x0000561ad6775eb0>)

u.instance_eval do
  def hello
    'Hello World!'
  end
end

u.hello # => 'Hello World!'
```

Method **instance_eval** can take either a string or a block as parameters. There is also the **instance_exec** method, which works the same but also allows us to pass arguments.

<br>

### <a name="defineMethod">9. Define Method</a>
Method **instance_eval** is used for create new methods at runtime.

``` Ruby
class User
  def method_missing(method)
    self.class.define_method(method) { puts 'Hello World' }
    
    puts 'New method created!'
  end
end

u = User.new

u.hello # => 'New method created!'
u.hello # => 'Hello World!'
```

