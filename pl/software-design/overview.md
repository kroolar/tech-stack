# Podstawy OOP

### Wstęp

#### Klasa
W językach zorientowanych obiektowo, klasą nazwiemy kod na podstawie, którego tworzone są obiekty.
Można o niej myśleć jak o pewnego rodzaju szablonie do tworzenia obiektów, która może dostarczać początkowe wartośći oraz funkcjonalności.

``` Ruby
class Human
  attr_reader :name

  def initialize(name)
    @name = name
  end
  
  def hello(greeting: 'Hello!')
    "${greeting} My name is #{name}"
  end
end
```

#### Obiekt
Obiekt jest główną częścią języka Ruby(wszystko w Ruby jest obiektem).
Tworzy się go na podstawie klasy.

``` Ruby
artur = Human.new('Artur')
```

Obiekt jest złożony z właściwości(atrybutów):

``` Ruby
artur.name # => 'Artur'
```

Oraz z zachowania(metod):

``` Ruby
artur.hello # => Hello! My name is Artur
```

#### Metoda
Metoda określa zachowanie danego obiektu.
Może przyjmować parametry, które zmieniają jej działanie.
W języku Ruby jeśli żadna wartość nie zostanie jawnie zwrócona metoda zwraca wartość ostaniego wyrażenia.

``` Ruby
artur.hello(greeting: 'Good Morning!') # => Good Morning! My name is Artur
```

#### Instancja
Instancją danej klasy nazwiemy obiekt utworzony na podstawie tej klasy.
W powyższym przypadku, obiekt artur jest instancją klasy Human

### Cztery Zasaday OOP

#### Enkapsulacja

#### Abstrakcja
Abstrakcja pozwala nam tworzyć rozwiązania danego problemu wzorując się na przykładach z życia codziennego. Koncepcja ta odnosi się do tworzenia rozwiązań, które są łatwo rozumiane przez człowieka.

#### Dziedziczenie
Dziedziczenie to zdolnośc dzielenia się swoim zachowaniem z innymi klasami.
Klasę, która dziedzicy z innej klasy nazywamy klasą nadrzędną, a klasa, która dziedziczy jest określana klasą podrzędna lub podklasą.
W języku Ruby klasa może bezpośrednio dziedziczyć tylko z jednej klasy.

``` Ruby
class Mammal
  attr_reader :age

  def initialize(age)
    @age = age
  end
end

class Human < Mammal; end

class Dog < Mammal; end

human = Human.new(age: 25)
dog = Dog.new(age: 7)

human.age # => 25
dog.age # => 7
```

Moduły w Ruby są rozwiązaniem problemu wielokrotnego dziedziczenia. Są kontenerami na metody, które później można dołączać do innych klas. Rozwiązanie takie nazywa się mixin-em.
Konwencja nazywania mixinów polega na dodawaniu przyrostka -able do nazwy modułu.

``` Ruby
module Speakable
  def say(word)
    word
  end
end

class Human < Mammal
  include Speakable
end

human = Human.new(age: 25)
human.say('I can talk!') # => I can talk!
```

Super
Słowo kluczowe Super wywołuje metodę w klasię nadrzędnej o tej samej co metoda w której wywoływane jest super.
class Human < Mammal
  def initialize(age:, name:)
    super(age)
    @name = name
  end
end

human = Human.new(age: 25, name: 'Artur')
human.age # => 25
human.artur # => 'Artur'

#### Polimorfizm

The Four Principles of Object-Oriented-Programming (OOP)
- Encapsulation
- Abstraction
Abstrackaj pozwala nam na tworzenie rozwiązanie jakiegoś problemu za pomoca tworzenia koncepcji z rzeczywistego świata przez co staję się to dla nas ławtiwejsze do zrozumienai. Ma to być dobre dla człowieka a nie dla maszyny.
Musimy patrzeć na to jak to opisujemy a nie jak to działa
Patrzymy na obiekty, które mają jakiś stan a nie na zachowanie.
I zależności między nimi
- Inheritance
- Polymorphism

### Abstrakcja

public private protected

### Polimorfizm

Setter and getter
super
self
