# Method Lookup Chain

Method Lookup Chain jest procesem, który odpowiada za znalezienie odpowiedniej metody, którą chcemy uruchomić.

1. Singleton methods
2. Prepend modules
3. Instance methods
4. Include modules
5. Parent class
6. Object, Kernel and BasicObject
7. Method missing
8. Super
9. Extend


1. Instance methods
Metody instancji to pierwsze miejsce, gdzie Ruby szuka metody. Czym jest metoda instancji> Jest to metoda, która została utworzona tylko i wyłącznie dla jednego obiektu/instancji danej klasy.

``` Ruby
class Dog
end

dog = Dog.new
dog.me # => NoMethodError
  
def dog.me
  'asd'
end
```

2. Prepend modules
Ruby nie wspiera wielokrotnego dziedziczenia ale umożliwa to za pomocą modułów. Popularnie zwanych jako mixiny. Za pomocą metody prepend możemy dołączać moduły do klas i korzystać z nich tak jakby były wbudowane.

3. Instance methods
Jeśli nie stworzyliśmy żadnych metod instancji oraz nie dołączyliśmy żadnych modułów to zostanie uruchomiona metoda, która została zdefiniowana w klasie. Najczęściej metody są uruchamiane właśnie z tego miejsca.

4. Include methods
  Za pomocą include możemy dołączać moduły tak samo jak w przypadku prepend. Jedyną róznicą jest to, że zostaą wyszukane dopiero wtedy kiedy metoda o takiej samej nazwie nie została zdefiowana w jako metoda instancji
  
7. Parent class methods
  Jeśli Ruby nie natrafił na daną metode do tego czasu będzie sprawdzał czy metoda z której dziedziczy dana klasa nie posiada takiej klasy. Jeśli nie to będzie szedł w góre i sprawdzała czy rodzic metoda z której dziedziczy nie ma takiej metody i tak dalej i tak ddalej.
 
9. Object, Kernel, BasicObject
  A co jeśli klasa nie dziedziczy z żadnej klasy? Tak naprawdę nawet klasa, która jawnie nie dziedziczy z żadnej klasy dziedziczy z klasy Object.
  Natomiast klasa object dzidziczyz klasy BasicObject.
  Między nimi znajduję się jeszcze moduł kernel
 
11. Method Missing
  Jeśli żaden moduł ani klasy po drodze nie trafi na daną metoda to zostanie uruchomiona metoda missing_method najpierw w głównej kklasie. Metoda ta służy najczęściej do metaprogramowania ale może być użyta w dowolnym celu. Jest to zwykła metoda, która zostaje uruchomiona w momencie kiedy nie można uruchomić metody.
  Jeśli method missing nie zostanie zdefiniowana w klasie to interpreter będzie jej szukał w klasie nadrzędnej, aż dojdzie do samej góry/
  
13. NoMethodError
  Jełśi nic nie znajdzie zostanie uruchomiony NoMethodError



10. NoMethodError
Co jeśli dany obiekt ani, żadna klasa nadrzędna nie posaida, żadnej metody. Wtedy to zostanie zwrócony NoMethodError.

2. Method missing
Jeśli Ruby nie znajdzie, żadnej metody będzie wywoływał method_missing najpierw w tej samej klasie, a jeśli tam jej nie znajdzie to w każdej następnej. Metoda ta najczęściej jest używana w przypadku metaprogramowania.

4. Object, Kernel and BasicObject

dog = Dog.new

dog.equal? 'as' => false
Jakim cudem to działa?

Ponieważ
Każda klasa dziedziczy z klasy Object, która dziedziczy z BasicObject. Możemy to sprawdzić następująco.
Dog.superclass
Dog.superclass.superclass

Jak widzimy dalej już nic nie ma
Dog.superclass.superclass.superclass

Jednak to nie są wszyscy rodzice z których dziedziczy Dog. Jeśli chcemy to sprawdzić musimy uruchomić metode ancestors.

Dog.ancestors => [Dog, Object, Kernel, BasicObject]

Jak to możliwe? Ponieważ Kernel nie jest klasą tylko modułem możemy to sprawdzić

Dog.ancestors.map { |d| "#{e.class}: #{e}" } => ["Class: Dog", "Class: Object", "Module: Kernel", "Class: BasicObject"]

W jeżyku Ruby występuje tylko pojedyncze dziedziczenie ale dzięki modułom możemy zmieniać zachowanie klas tak jakbyśmy mieli wielokrotne dziedziczenie.

3. Parent class
class Animal
  def me
    ;asd
  end
end

class Dog < Animal
end

dog = Dog.new

dog.me

Jeśli klasa nie ma metody będzie jej szukał w metodzie rodziców.


5. Singleton methods

Method Lookup jako pierwsze szuka w singleton methods.
Singleton method jest metodą, która została utworzona tylko dla konkretnej instancji.

``` Ruby
class Dog
  def me
    puts 'I am a Human'
  end
end

artur = Human.new
bartek = Human.new

def artur.me
  puts "I'm Artur"
end

artur.me
bartek.me
```

2. Prepend modules
``` Ruby
module Something
  def me
    'I am a new module'
  end
end

class Dog
  prepend Something
  
  def me
    I am
  end
end
```

3. Metody zdefiniowane w klasie
4. Include modules
5. Parents classes and modules -> Object -> Kernel -> BasicObject 
6. Method missing
7. NoMethodError


9. Extend module
10. Method in class
11. Included modulesuby


