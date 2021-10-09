# Ruby 3.0

1. [Performance](#performance)
2. [Parallelism & Concurrency](#pc)
3. [Static Analysis](#staticAnalysis)
4. [Others](#others)

### <a name="performance">1. Performance</a>

JEst 3 raz yszybszy od Ruby 2.0

CPU optimatization 
Poprawa MJIT, który by już przedstawiony w Ruby 2.6. Czym jest MJIT. JIT jest to Just-In-Time compiler, który konwertuje powtarzający się kod na kod bajtowy, który potem 

Memory optimization
Zaszły istotne zmiany w Garbage collector

Wprowadzono Garbage Compaction, który był już dostępny w Ruby 2.7 ale zostałc całkowicie zautomatyzowany w nowej wersji

2. Parallelism and Concurency

FIbers

3. Static analysis
RBS

RBS to język, który opisuje strukture programu Ruby i to jak zdefiniowane są klasy, metody, są zdefiniowane.

RBS pozwala pisać definicje klas, modułów, metod, zmiennych, typów zmiennych oraz dziedziczenia. Wspiera również powszechnie stosowane wzorce w  Ruby oraz unions and duck typing

``` Ruby
# user.rbs

class User
  attr_reader name: String
  attr_reader age: Integer

  def initialize: (name: String, age: Integer) -> void
end
```

Typeprof


4. Other

#### One-line pattern mathcing(Experimental)

Dodano operator =>, który może być używany jako przypisanie prawostronne

``` Ruby
'John' => name
name # => 'John'

{ email: 'j.doe@mail.com', age: 25 } => { age: }
age => 25
```

Operator in zwraca tera true lub false



#### Endless method definition(Experimental)

Pozwala tworzyć jednolinijkowe metody bez użycia keyword end

Zamiast takiego kodu
``` Ruby
def double(number)
  number * 2
end
```

Możemy zrobić coś takiego
``` Ruby
def double(number) = number * 2

triple(3) # => 6
```

#### Except Hash method

Metoda except, która dotychczas była dostępna tylko w Railsach jest dostępna w Ruby.
``` Ruby
user = {
  name: 'John',
  email: 'john.doe@mail.com',
  age: 35
}

user.except(:age) # => { 
```
