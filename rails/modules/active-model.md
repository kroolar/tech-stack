# Active Model

The Active Model contains various modules that are used in Active Record.

### Attribute Methods

They let you add prefixes and suffixes to class attributes.

``` Ruby
class User
  include ActiveModel::AttributeMethods

  attribute_method_prefix 'reset_'
  define_attribute_methods 'name'

  attr_accessor :name

  private
    def reset_attribute(attribute)
      send("#{attribute}=", "")
    end
end

user = User.new
user.name = "John Doe"
user.reset_name 
user.name = ""
```

### Callbacks

They allow you to add callbacks just like in Active Record.

``` Ruby
class User
  extend ActiveModel::Callbacks

  define_model_callbacks :update

  before_update :do_something

  def update
    run_callbacks(:update) do
    end
  end

  def do_soemthing; end
end
```

### Conversion

If the methods **persisted?** and **id?** will be added to the object you will be able to use the conversion method on them.

``` Ruby
class User
  include ActiveModel::Conversion

  def persisted?
    false
  end

  def id
    nil
  end
end

user = User.new
user.to_key # => nil
```

### Dirty

Thanks to this module, we can check whether the model has been changed.

``` Ruby
class User
  include ActiveModel::Dirty
end

user = User.new
user.name = 'John Doe'
user.changed? # => true
```

### Validations

Adds the ability to validate objects.

``` Ruby
class User
  include ActiveModel::Validations
  
  attr_accessor :name
  
  validates :name, presence: true
end

user = User.new
user.valid? # => false
```

### Naming

It adds many methods that allow for better name management, which makes working with the router much easier. The module defines a method, **model_name**, which is mostly based on the **ActiveSupport::Inflector** module.

``` Ruby
class User
  extend ActiveModel::Naming
end

User.model_name.name # => "user"
User.model_name.plural # => "users"
```

### Model

The model adds the ability to work with **Action Pack** and **Action View**. This allows the object to access functions such as:

- model name introspection
- conversions
- translations
- validations

It also allows you to create objects based on hashes of attributes such as **Active Record**.

``` Ruby
class User
  include ActiveModel::Model
end

User.new(name: "John Doe", age: 25)
```

### Serialization

It allows basic serialization of your objects.

``` Ruby
class Person
  include ActiveModel::Serialization
end
```

### Transaltion

It allows you to integrate the model with the Rails internationalization framework (i18n).

``` Ruby
class User
  extend ActiveModel::Translation
end
```

### Lint Tests

It allows you to check if the object is compatible with the Active Model API.

``` Ruby
class User
  include ActiveModel::Model
end
```

### SecurePassword

It is based on the **bcrypt** gem, so it must be added to gemfile in order to use it properly. Responsible for password management.

``` Ruby
class User
  include ActiveModel::SecurePassword
  has_secure_password
end

user = User.new
user.valid? # => false

user.password = "1234"
user.valid? # => true
```

### Sources
- https://guides.rubyonrails.org/active_model_basics.html
