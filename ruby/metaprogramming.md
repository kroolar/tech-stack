# Metaprogramming

- [Overview](#overview)
- [Method Missing](#methodMissing)
- [Send](#send)
- [Instance Methods](#instanceMethods)

- Respond to?
- Instance variables
- methods
- ancestors
- define_method
- instance exec
- instance eval

### <a name="overview">Overview</a>
Metaprogramowanie to tworzenie programów, które mogą tworzyć i modyfikować kod w trakcie działania programu. Ruby dostarcza nam narzędzia, które pozwalają na metaprogramowanie.

### <a name="methodMissing">Method Missing</a>
Jedną z najpopularniejszych metod używaną w metaprogramowaniu jest **method_missing**. Metoda ta pozwala wykonywać jakaś operację jeśli nie znajdzie odpowiadającej metody. Do **method_missing** musimy przekazać wywoływaną metodę oraz dodatkowo możemy dołączyć jej argumenty oraz blok.

Poniższy kod przedstawia możliwą implementacje klasy **ActiveRecord**, która pozwala na wywoływanie wielu metod mimo tego, że nie zostały one zdefiniowane w klasie **ActiveRecord**.

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

### <a name="send">Send</a>

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

### <a name="instanceMethods">Methods</a>

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

``` Ruby
  def complete_all
    all_methods = self.class.instance_methods(false) - [:complete_all]

    all_methods.map { |method| send(method) }
  end
```


Respond_to?
method_missing
send
instance_variables
