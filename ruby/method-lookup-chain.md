# Method Lookup Chain
Method Lookup Chain is a process that is responsible for finding the appropriate method that we want to run.

1. [NoMethodError](#noMethodError)
2. [Method Missing](#methodMissing)
3. [Object, BasicObject](#basicObject)
4. [Parent Class](#parentClass)
5. [Include Modules](#includeModules)
6. [Instance Methods](#instanceMethods)
7. [Prepend Modules](#prependModules)
8. [Singleton Methods](#singletonMethods)
9. [Extend Modules](#extendModules)

### <a name="noMethodError">1. NoMethodError</a>
If we call a method that is not defined then **NoMethodError** will be returned.

``` Ruby
class Human; end

john = Human.new
john.hello # => NoMethodError: undefined method `hello' for #<Human:0x000055cf33cc59b8>
```
<br>

### <a name="methodMissing">2. Method Missing</a>
Before **NoMethodError** is raised, **method_missing** is run. This method is run whenever Ruby cannot find a matching method. This method is most often used in metaprogramming.

``` Ruby
class Human
  def method_missing(method)
    "Method 'method' not found"
  end
end

john = Human.new
john.hello # => "Method 'hello' not found"
```
<br>

### <a name="basicObject">3. Object, BasicObject</a>
We want to check our object id. How is it possible if we haven't created such a method?

``` Ruby
class Human; end

john = Human.new
john.object_id # => 47319130769440
```
<br>

Ruby looks for the parent class and all parent classes next. But in case a class does not explicitly inherit from another class, it inherits from **Object** and therefore we can use the **object_id** method.

``` Ruby
Human.superclass # => Object
```
<br>

The **Object** class inherits from **BasicObject**, which is the parent of all classes in Ruby.

``` Ruby
Human.superclass.superclass # => BasicObject
Human.superclass.superclass.superclass # => nil
```
<br>

### <a name="parentClass">4. Parent Class</a>
Before looking for a method in the **Object** and **BasicObject** classes, Ruby looks for a method in the all explicitly defined parent classes.

``` Ruby
class Mammal
  def hello
    'Hello from parent class'
  end
end

class Human < Mammal; end

john = Human.new
john.hello # => "Hello from parent class"
```
<br>

### <a name="includeModules">5. Include Modules</a>
In Ruby, there is only a single inheritance, but thanks to modules, we can change the behavior of classes as if multiple inheritance was possible.

With **include**, we can include modules in a given class. Thanks to this, we have access to all methods defined in the module.

``` Ruby
module Talkable
  def hello
    'Hello from Talkable module'
  end
end

class Human < Mammal
  include Talkable
end

john = Human.new
john.hello # => Hello from Talkable module
```
<br>

Coming back to the **Object** class, it is worth mentioning that the **Kernel** module is also included to the **Object** class. We didn't see this when checking the parent classes, but we can check it with the **ancestors** method.

``` Ruby
Object.ancestors => [Object, Kernel, BasicObject]
```
<br>

### <a name="instanceMethods">6. Instance Methods</a>
The most commonly used methods are **instance methods**. These are the usual methods that are defined in the class.

``` Ruby
module Talkable
  def hello
    'Hello from Talkable module'
  end
end

class Human < Mammal
  include Talkable

  def hello
    'Hello from instance method'
  end
end

john = Human.new
john.hello # => 'Hello from instance method'
```
<br>

### <a name="prependModules">7. Prepend Modules</a>
**Prepend** allows modules to be included in a class similar to **include**, except that the methods defined in this module will take precedence over the **instance methods**.

``` Ruby
module Talkable
  def hello
    'Hello from Talkable module'
  end
end

class Human < Mammal
  prepend Talkable
  
  def hello
    'Hello from instance method'
  end
end

john = Human.new
john.hello # => 'Hello from Talkable module'
```
<br>

### <a name="singletonMethods">8. Singleton Methods</a>
A **singleton method** is one that has been defined only for a specific instance. This method is rarely used and takes precedence over all and other methods.

``` Ruby
module Talkable
  def hello
    'Hello from Talkable module'
  end
end

class Human < Mammal
  prepend Talkable

  def hello
    'Hello from instance method'
  end
end

john = Human.new
john.hello # => 'Hello from Talkable method'
  
def john.hello
  'Hello from singleton method'
end

john.hello # => 'Hello from singleton method'
```
<br>

### <a name="extendModules">9. Extend Modules</a>
In Ruby, we can also create class methods.

``` Ruby
class Human
  def self.hello
    'Hello from class method'
  end
end

Human.hello # => 'Hello from class method'
```
<br>

In the case of class methods, we can also attach modules to them using **extend**.

``` Ruby
module Talkable
  def hello
    'Hello from extended module'
  end
end

class Human
  extend Talkable
end

Human.hello # => 'Hello from extended module'
```
<br>

**Extend** is similar to include. Therefore, the methods of the class are checked first, and then the methods in the module. Ruby has no equivalent for prepend when it comes to class methods.

``` Ruby
module Talkable
  def hello
    'Hello from extended module'
  end
end

class Human
  extend Talkable
  
  def self.hello
    'Hello from class method'
  end
end

Human.hello # => 'Hello from class method'
```
