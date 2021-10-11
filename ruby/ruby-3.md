# Ruby 3.0

1. [Performance](#performance)
2. [Parallelism & Concurrency](#pc)
3. [Static Analysis](#staticAnalysis)
4. [Others](#others)

### <a name="performance">1. Performance</a>
As promised, Ruby's 3.0 version is 3 times faster than Ruby 2.0. This was done thanks to the introduction of several CPU and Memory improvements.

#### CPU Performance 
**MJIT** was introduced in Ruby 2.6. **MJIT** stands for Method Based Just-in-Time compiler. By default, Ruby is compiled into YARV instructions, which are then run by a virtual machine. **MJIT** compiles repetitive code directly into bytecode, which speeds up the compiler's work.

#### Memory Performance
Ruby 3 also brought some improvements to the garbage collector area. In version 3, the **Garbage Compaction** that was introduced in Ruby 2.7 has been improved. Compared to the old version, the new one has been completely automated to ensure proper memory use. Additionally, it groups scattered objects into one memory location so that this memory can later be used by larger objects.

### <a name="pc">2. Parallelism & Concurrency</a>
### Ractors(Experimental)

### <a name="staticAnalysis">3. Static Analysis</a>

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


### <a name="others">4. Others</a>


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
