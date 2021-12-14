# Active Record

Active Record is responsible for representing the data and its logic. It allows you to easily use the database.

### Conventions

According to the conventions used in Rails, models should be named singular as opposed to table name, which is written in plural.

### CRUD

Active Record automatically creates methods that allow you to manage data based on the acronym CRUD, which stands for Create, Read, Update, Delete.

``` Ruby
# Create new user
User.create(name: 'John Doe')

# Find user by name
user = User.find_by(name: 'John Doe')

# Update user's name
user.update(name: 'Jane Doe')

# Remove user
user.destroy
```

### Validations

Active Record also provides validation of attributes, thanks to which we will not be able to write incorrect data to the database. The following example shows a validation that forces the name attribute to exist.

``` Ruby
class User < ApplicationRecord
  validates :name, presence: true
end

user = User.new
user.save # => false
```

The above action will return false because the model fails the validation. There are also equivalents with an exclamation point that will return an error instead of false.

### Callbacks

Callbacks are used to trigger specific actions during the model lifecycle.

### Migrations

Active Record also introduces its own DSL to help manage the database schema.

``` Ruby
class CreatePublications < ActiveRecord::Migration[6.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :description
      t.timestamps
    end
    
  end
end
```

### Sources
- https://guides.rubyonrails.org/active_record_basics.html
- https://guides.rubyonrails.org/active_record_migrations.html
- https://guides.rubyonrails.org/active_record_validations.html
- https://guides.rubyonrails.org/active_record_callbacks.html
- https://guides.rubyonrails.org/association_basics.html
- https://guides.rubyonrails.org/active_record_querying.html
- https://guides.rubyonrails.org/active_record_callbacks.html
- https://api.rubyonrails.org/files/activerecord/README_rdoc.html
