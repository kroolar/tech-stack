# Active Record

Active Record jest odpowiedzialny za reprezentowanie danych oraz ich logiki. Pozwala w prosty sposób korzystać z bazy danych.

### Conventions

Zgodnie z konwecjami używanymi w Railsach modele pow

### CRUD

ACtive REcord automatycznie tworzy metody, któ©e pozwalają zarządzać danymi na podstawie akronimu CRUD, który oznacza Create, Read, Update, Delete.

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

Active Record zapewnia także walidację atrybutów dzięki czemu nie będziemy w stanie zapisać niepoprawnych danych do bazy danych. Poniższy przykład pokazujęwalidację, któ©a wymusza istnienie atrybutu name.

``` Ruby
class User < ApplicationRecord
  validates :name, presence: true
end

user = User.new
user.save # => false
```

Powyższa akcja zwróci false ponieważ model nie spełnia walidacji. Istnieją też odpowiedniki z wykrzyknikiem, które zamiast false wyrzucą błąð.

### Callbacks
### Migrations
