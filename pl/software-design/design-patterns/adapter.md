### Adapter

#### Opis
Strukturalny wzorzec projektowy, który pozwala pracować ze sobą dwóm niekompatybilnym obiektom.

#### Problem

``` Ruby
class Shop
  def sell(amount: 1, product:)
    product.price * amount
  end
end

class Product
  attr_reader :name, :price

  def initialize(name:, price:)
    @name = name
    @price = price
  end
end

class Decoration
  attr_reader :value

  def initialize(value:)
    @value = value
  end
end

shop = Shop.new
table = Product.new(name: 'table', price: 99)
christmas_ball = Decoration.new(value: 2)

shop.sell(product: table) # => 99
shop.sell(product: christmas_ball) # => NoMethodError
```

W takim przypadku poiwnniśmy opakować klasę Decoration klasą o nazwie adapter oraz zapewnić interfejs dzięki, któremu opakowany obiekt będzie mógł się komunikować z inną klasą.

``` Ruby
DecorationAdapter < Decoration
  def price
    @value * 5
  end
end

decoration_adapter = DecorationAdapter.new(value: 2)
shop.sell(amount: 2, product: christmas_ball) # => 4
```
#### Plusy i Minusy
