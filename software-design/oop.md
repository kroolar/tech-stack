# Object Oriented Programming

1. [Overview](#overview)
2. [Four Pillars of OOP](#fourPillars)
3. [SOLID](#solid)
4. [Principles](#principles)

### <a name="overview">1. Overview</a>

OOP to rodzaj programowania w którym programy definiuje się za pomocą obiektów. Programowanie obiektowy wprowadza trochę nowej terminologi:


#### Class
Jest opisem(blueprint) na podstawie, którego można tworzyć obiekty

``` Ruby
class Car
end
```

#### Object
Obiekt jest podstawowym budulcem w językach obiektowych. W Ruby wszystko jest obiektem.

``` Ruby
car = Car.new
```

#### Method
Metoda jest właściwością obiektu, który określa jego zachowania.

``` Ruby
class Car
  def drive
  end
end

car = Car.new
car.drive
```

#### Attributes
Attrybuty są właściwośćią danego obiektu, który określa konkretny stan.

``` Ruby
class Car
  attr_reader :brand
  
  def initialize(brand)
    @brand = brand
  end
end

bmw = Car.new('BMW')
bmw.brand # => "BMW"
```

#### Instance
Instancja jest określeniem danego obiektu w kontekście do jego klasy.(np. Obiekt BMW jest isntancją klasy Car)

### <a name="fourPillars">2. Four Pillars</a>

#### Encapsulation
#### Abstraction
#### Inheritance
Termin ten odnosi się do możliwośći dziedziczenia pwenych cech i właściwości z innych klas. Stworzymy klasę Car, i umieścimy w niej metodę odpowiedzialna za uruchomienie silnika.

``` Ruby
class Car
  def start_engine
    puts "The engine has started"
  end
end
```

Teraz natomiast chcemy utworzyć klasę motocykl, która także powinna zawierać metodę, która pozwoli na uruchomienie silnika. Oprócz tego chcemy także dodać metodę, która pozoli nam zatrzymać silnik.

Zamiast dodawać te same metody w dwóch róznych miejscach, możemy je wyeksportować do wspólnej klasy Vehcile, która będzie mogła przetrzymywać wartości wspólne dla wszystkch pojazdów, a następnie za pomocą dziedziczenia udostępnić jej metody klasą podrzednym.

``` Ruby
class Vehicle
  def start_enging
    puts "The engine has started"
  end
  
  def stop_engine
    puts "The engine has stopped"
  end
end

class Car < Vehicle; end
class Motorcycle < Vehicle; end

car = Car.new
motorcycle = Motorcycle.new

car.start_engine # => "The engine has started"
motorcycle.stop_engine # => "The engine has stopped"
```
W jezyku Ruby dostępne jest tylko pojedyncze dziedziczenie co oznacza, że klasą może odziedziczyć tylko i wyłącznie z jednego rodzica. Jednakże Ruby pozwala osiągnąć wielokrotne dziedzicznie dołączając moduły do danej klasy.

#### Polymorphism

Polimorfizm oznacza zdolność do przyjmowania wielu form. W kontekście programowania ejst to najczęściej udostępnianie jednego wspólnego interfejsu. który może być używany przez różne obiekty. W języku Ruby możemy osiągnąć polimorfizm na trzy różne sposoby

##### Inheritance

``` Ruby
class Vehicle
  def type
    raise NoImplementedError
  end
end

class Car < Vehicle
  def type
    puts ''
  end
end

class Motorcycle < Vehicle
end
```

##### Duck Typing

### <a name="solid">3. SOLID</a>

#### Single Responsibility Principle (SRP)
Klasa powinna być oodpowieidzialny tylko i wyłącznie za jedną rzecz. Nie Powinien istnieć więcej niż jeden powód do modyfikacji klasy.

#### Open/Closed Principle (OCP)
Klasy powinny być otwarte na rozszerzenia i zamknięte na modyfikacje.

#### Liskov Substitution Principle (LSP)
Obiekty, które dziedzczą z klasy bazowej powinny być w stanie zastępować obiekty klasy bazowej bez zmiany działania programu.

#### Interface Segregation Principle (ISP)

#### Depedency Inversion Principle (DIP)

### <a name="principles">4. Principles</a>

### KISS
Keep it simple stupid
### YAGNI
### DRY
Don't repeat yourself
