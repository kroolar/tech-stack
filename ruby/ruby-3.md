# Ruby 3.0

1. [Performance](#performance)
2. [Parallelism & Concurrency](#pc)
3. [Static Analysis](#staticAnalysis)
4. [Others](#others)

### <a name="performance">1. Performance</a>
As promised, Ruby's 3.0 version is 3 times faster than Ruby 2.0. This was done thanks to the introduction of several CPU and Memory improvements.

#### CPU Performance 
**MJIT** was introduced in Ruby 2.6. **MJIT** stands for Method Based Just-in-Time compiler. By default, Ruby is compiled into YARV instructions, which are then run by a virtual machine. **MJIT** compiles repetitive code directly into bytecode, which speeds up the compiler's work.

#### Memory Performance
Ruby 3 also brought some improvements to the garbage collector area. In version 3, the **Garbage Compaction** that was introduced in Ruby 2.7 has been improved. Compared to the old version, the new one has been completely automated to ensure proper memory use. Additionally, it groups scattered objects into one memory location so that this memory can later be used by larger objects.

### <a name="pc">2. Parallelism & Concurrency</a>

#### Ractors(Experimental)
Normally, Global VM Lock is responsible for blocking threads and only allows one thread to run at a time. In the Ruby 3, a new class that improves Ractors parallelism. Each ractor has its own lock, thanks to which, by creating several ractors, we are able to really use parallelism. Ractors can have more than one thread, so in the case of threads running in Ractor we are still talking about concurrency, but Ractory work in parallel with each other.

``` Ruby
ractor = Ractor.new { puts "Hello World!" }

ractor.take
```

#### Fiber Scheduler(Experimental)

The scheduler was created to improve threads managment. It allows you to intercept blocking operations. It is an interface that allows you to wrap your code with gems like **EventMachine** or **ASync**. It allows you to separate the implementation of async from the application code.

### <a name="staticAnalysis">3. Static Analysis</a>

#### RBS

RBS is a language that describes strcture of Ruby code and how to define its class and methods. RBS allows you to write classess, modules, methods, variables and inheritance definitions. It also supports duck typing.

``` Ruby
# user.rbs

class User
  attr_reader name: String
  attr_reader age: Integer

  def initialize: (name: String, age: Integer) -> void
end
```

RBS It is programmed in such a way that it does not force us to use it, but we get a new tool that allows us to create better software, so we can easily introduce it in old projects.

#### Advantages of typing in Ruby:

- **Finding Bugs**: Typing helps finding more bugs faster.
- **NIL**: Type checkers significantly improve work with nil, so they can check whether the value can be nil or should be given, which allows for less frequent use of the navigational safety operator.
- **Better IDE integration**: Parsing RBS files gives our IDE a better understanding of how our code should work

### <a name="others">4. Others</a>

#### One-line pattern mathcing(Experimental)

Added new operator **=>,** that can be using as a right-way assigment.

``` Ruby
'John' => name
puts name # => 'John'

{ email: 'j.doe@mail.com', age: 25 } => { age: }
puts age => 25
```

#### Find pattern
``` Ruby
users = [
  { name: 'Oliver', role: 'CTO' },
  { name: 'Sam', role: 'Manager' },
  { role: 'customer' },
  { name: 'Eve', city: 'New York' },
  { name: 'Peter' },
  { city: 'Chicago' }
]

users.each do |person|
  case person
  in { name:, role: 'CTO' }
    p "#{name} is the Founder."
  in { name:, role: designation }
    p "#{name} is a #{designation}."
  in { name:, city: 'New York' }
    p "#{name} lives in New York."
  in {role: designation}
    p "Unknown is a #{designation}."
  in { name: }
    p "#{name}'s designation is unknown."
  else
    p "Pattern not found."
  end
end

"Oliver is the Founder."
"Sam is a Manager."
"Unknown is a customer."
"Eve lives in New York."
"Peter's designation is unknown."
"Pattern not found."
```

#### Endless method definition(Experimental)

Allow to create one-line methods without **end** keyword

Old way:

``` Ruby
def double(number)
  number * 2
end
```
New way:

``` Ruby
def double(number) = number * 2

triple(3) # => 6
```

#### Except Hash method

Except method, that was only available in Rails is now availabel in Ruby.

``` Ruby
user = {
  name: 'John',
  email: 'john.doe@mail.com',
  age: 35
}

user.except(:age) # => { name: 'John', email: 'john.doe@mai;.com' }
```

#### Arguments forwarding

Argument forwarding **...** is a shortcut that allows you to pass various arguments.

Old way:

``` Ruby
class User
  def initialize(*args, **kwargs, &block)
    create(*args, **kwargs, &block)
  end
end
```

New way:

``` Ruby
class User
  def initialize(...)
    create(...)
  end
end
```

