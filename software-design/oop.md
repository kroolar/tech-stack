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
Jest procesem, który pozwala opakowywać pewne dane w pojedyncze jednostki.

W poniższym przykładzie mamy jedną klasę App, która reprezentuje całą naszą aplikacje. Klasa ta posiada kilka metod odnoszących się do użytkowników oraz pracowników.

``` Ruby
class App
  def create_user(user, params)
    # Do something
  end
  
  def update_employee(employee, params)
    # Do something
  end
  
  def delete_user(user)
    # Do something
  end
end
```
Powołując się na enkapsulacje możemy je podzielić na mniejsze jednostki

``` Ruby
class User
  def create(params)
    # Do something
  end
  
  def delete
    # Do something
  end
end

class Employee
  def update(params)
    # Do soemthing
  end
end
```

#### Abstraction

Abstrakcja pozwala ukryć detale, które nie są istotne takie jak implementacja i pokazać tylko te które są niezbędne. Użytkownik nie musi mieć dostepu do wszystkich części kodu wystarczy mu prosty interfejs z którego będzie korzystał.

``` Ruby
class CRM
  def users
    get('/users')
  end
  
  private
  
  def access_token
    # Do something
  end
  
  def get(method)
    response = HTTParty.get(method, access_token)
    
    response.body
  end
end
```
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

Polimorfizm oznacza zdolność do przyjmowania wielu form. W kontekście programowania określa, że jedna czynność może być wykonywana na różne sposoby. W języku Ruby możemy osiągnąć polimorfizm na trzy różne sposoby

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

### Law of Demether
Czasem znana jako Principle of least knowledge. Określa, że obiekt powinien rozmawiać tylko i wyłącznie ze swoimi najlbiższymi obiektami. Obiekt nie powinien wykonywać metody prze inny obiekt.

W Rails przez asocjacje często tworzymy ogromne niepotrzebne łanuchy metod. Weźmy ten przykład.

``` Ruby
class User < ApplicationRecord
  belongs_to: company
end

class Company < ApplicationRecord
  has_many :users
end
```
Comapny przechowuje swoją nazwę, więc jeśli chcemy wywołać nazwę firmy z poziomu użytkownika możemy to zrobić w taki sposób.

``` Ruby
users.company.name
```
To jest właśnie złamanie prawa Law of Demeter. Obiekt nie powinien kontaktować się z metodami innych obiektów. Jeśli chcemy pobrać nazwę firmy powinniśmy zrobić to w ten sposób.

``` Ruby
class User < ApplicationRecord
  belongs_to: company
  
  def company_name
    company.name
  end
end

user.company_name
```

Railsy dodatkowo są wyposażone w tzw. delegatory, które pozwalają skrócić ten zapis. Odpowiednikiem powyższego przykłądu jest ten poniżej

``` Ruby
class User < ApplicationRecord
  belongs_to: company
  
  delegate :name, to: :company
end
```

### KISS
Keep It Simple, Stupid - Określa sposób projektowania w taki, żeby robić co jak najprośćiej, używająć jak naprostszych narzędzi bez żadnych udziwnień taka, żeby struktura nie zawierała niepotrzebnych elementów oraz, żeby każdy nawet najmniej uzdolniony z zespołu mógł to zrozumieć.

### YAGNI
You Aren't Gonna Need It - Odnośi się do nie tworzenia niepotrzebnego kodu. Czasem może się wydawać, że jakaś implementacja ma sens i może się przydać w przyszłości ale okazuje się, że jest nie działa zvyt dobrze, lub jest całkowicie niepotrzebna przez co trzeba refaktorować kod lub całkowicie go usunąc. Dlatego metoda ta mówi o tym, żeby odkładać pisanie kodu na później.

### DRY
Don't Repeat Yourself - Jak sama nazwa wskazuje odnosi się do tego, żeby sie nie powtarzać. Nie chodzi tu tylko o unikanie pisania powtarzającego się kodu ale także unikania powtarzających się czynności, które mogą zostać zautomatyzowane.
