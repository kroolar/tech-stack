### Builder

**Typ:** Kreacyjny

**Cel:** Pozwala budować złożone obiekty krok po kroku

#### Problem
Chcemy wybudować **Dom**. Każdy **Dom** posiada określoną liczbę **Okien**. W skład każdego domu może wchodzić **Ogród**. W każdym ogrodzie możemy dodatkowo posadzić kilka **Drzew** i zbudować **Basen**.

```Ruby
class House
  attr_accessor :windows, :garden
  
  def initialize(garden:, windows:)
    @garden = Garden.new
    @windows = windows
  end
end


class Garden
  attr_accessor :trees, :swimming_pool, size
  
  def initialize(swimming_pool: false, trees: 0, size: 0)
    @swimming_pool = false
    @trees = []
    @size = size
  end
end

class Tree
  attr_reader :type
  
  def initialize(type)
    @type = type
  end
end

house = House.new
apple_tree = Tree.new(:apple)
pear_tree = Tree.new(:pear)
garden = Garden.new(size: 100, trees: [apple_tree, pear_tree], swimming_pool: true)
house = House.new(windows: 10, garden: garden)
```

```Ruby
class HouseBuilder
  attr_reader :house
  
  def initalize
    @house = House.new
  end
  
  def windows=(quantity)
    @house.windows = quantity
  end
  
  def swimming_pool
    @house.garden.swimming_pool = true
  end
  
  def plant_apple_tree
    @house.garder.trees << Tree.new(:apple)
  end
end

builder = HouseBuilder.new
builder.windows = 10
builder.swimming_pool
5.times { builder.plant_apple_tree }
```

Plusy i Minusy
- Żłożone obiekty mogą być budowane krok po kroku
- Wzorzec może być wielokrotnie wykorzystywany do tworzenia nowych instancji
- Logika biznesowa jest oddzielona od logiki obiektu

Minusy
- Powiększamy złożoność projektu prze tworzenie kolejnej klasy
