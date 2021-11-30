# Singleton

Creational  pattern responsible for the fact that a class can only have one instance

### Problem

We want to log messages in the console. For this we will create a **Console** class similar to the one in JavaScript. For performance reasons, the class will be created only when it is needed and it will not be possible to create more than one instance.

``` Ruby
class Console
  @@instance = new
  
  def self.instance
    @@instance
  end
  
  def log(text)
    puts text
  end
  
  private_class_method :new
end

console = Console.new # => NoMethodError: private method 'new' called for Console:Class

Console.instance.log('Hello World!') # => Hello World
```

As you can see in the example above, we can't directly create a class with the new method, which is now private, and we need to use the instance method instead. By comparing two instances to each other, we can make sure that they are the same instance.

``` Ruby
console_one = Console.instance
console_two = Console.instance

console_one == console_two # => true
```

**Singleton** pattern is so popular that there is a **Singleton** module in the standard Ruby library, thanks to which we will not have to focus on pattern configuration.

``` Ruby
class Console
  include Singleton
  
  def log(text)
    puts text
  end
end
```

**Pros:**
- You are sure that there is only one instance of this class in entire app
- The object is initialized only when it is needed
- You have global access to this class

**Cons:**
- It can lead to a situation where objects know too much about each other
- In a multithreaded environment, this pattern can create multiple instances

**Sources:**
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/singleton.md
- https://refactoring.guru/design-patterns/singleton
- https://refactoring.guru/design-patterns/singleton/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-singleton-8c132da6a9ce
