### Adapter
#### Typ: Wzorzec Strukturalny
#### Kiedy stosować?
- Gdy chcemy wykorzystać istniejącą klasę, ale jej interfejs nie jest kompatybilny z resztą programu

#### Implementacja

#### Zalety
- Można oddzielić interfejs od logiki biznesowej (SRP)

#### Wady
- Zwiększona złożonośc kodu. Czasem lepiej zmienić adaptowaną klasę aby pasowała do reszty kodu

#### Podobne wzorce

#### Jak zaimplementować?
- Zdefiniuj jak ma wyglądać komunikacja między klasami
- 

``` Ruby
class Beer
  attr_reader :name, :price

  def initialize(brand:, price:)
    @brand = brand
    @price = price
  end
end

class Bartender
  def sell(amount: 1, product:)
    product.price * amount
  end
end

class Mug
  def initialize(size:, value:)
    @size = size
    @value = @value
  end
end

class MugAdapter < Mug
  def price
    @value * 3
  end
end
```

# Proxy
``` Ruby
class Product
  attr_reader :price

  def initialize(price:)
    @price = price
  end
end

class Client
  attr_reader :name, :table

  def initialize(name:, table:)
    @name = name
    @table = table
  end
end

class Bill
  attr_reader :balance, :table

  def initialize(table:)
    @balance = 0
    @table = table
  end

  def order(product)
    @balance += product.price
  end

  def pay(amount)
    @balance -= amount
  end
end

class BillProtectionProxy
  def initialize(bill:, client:)
    @bill = bill
    @client = client
  end

  def order(product)
    check_access
    return @bill.order(product)
  end

  def pay(amount)
    check_access
    return @bill.pay(amount)
  end

  private

  def check_access
    raise_warning unless bill_owner?
  end

  def bill_owner?
    @bill.table == @client.table
  end

  def raise_warning
    raise "#{@client.name} don't have access to this bill!"
  end
end
```
# Singleton
``` Ruby
class Bar
  @instance = new

  def self.instance
    return @instance
  end

  private_class_method :new
end

class Xyz
  @instance = 2
end

bar_one = Bar.instance
bar_two = Bar.instance

bar_one == bar_two # => true
```




# Builder

``` Ruby
class DrinkBuilder
  def initialize
    @drink = Drink.new
  end

  def add_ice(amount:)
    @drink.ingredients << Ingredient.new(:ice, amount:)
  end

  def add_lemon(amount)
    @drink.ingredients << Ingredient.new(:lemon)
  end

  def add_alcohol(type, amount)
    @drink.alcohol << Alcohol.new(type: type, amount: amount)
  end

  def price(price)
    @drink.price = price
  end

  def students_discount
    @drink.discount = true
  end
end
```
builder.add_lemon
builder.price(50)
builder.students_discount
