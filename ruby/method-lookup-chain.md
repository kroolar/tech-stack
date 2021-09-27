# Method Lookup Chain
Method Lookup Chain is a process that is responsible for finding the appropriate method that we want to run:

1. [NoMethodError](#noMethodError)
2. [Method Missing](#methodMissing)
3. [Object, Kernel, BasicObject](#basicObject)
4. [Parent Class](#parentClass)
5. [Include Modules](#includeModules)
6. [Instance Methods](#instanceMethods)
7. [Prepend Modules](#prependModules)
8. [Singleton Methods](#singletonMethods)

- [Super](#super)
- [Class Methods](#classMethods)
- [Extend](#extendModules)

### <a name="noMethodError">1. NoMethodError</a>
If we call a method that is not defined then _NoMethodError_ will be returned.

``` Ruby
class Dog
end

dog = Dog.new
dog.me # => NoMethodError: undefined method `me' for #<Dog:0x000055cf33cc59b8>
```

### <a name="methodMissing">2. Method Missing</a>
Before _NoMethodError_ is raised, _method_missing_ is run. This method is run whenever Ruby cannot find another method, and is used in meta-programming.

``` Ruby
class Dog
  def method_missing(method)
    'Method not found'
  end
end

dog = Dog.new
dog.me # => "Method not found"
```
<!-- 
### <a name="basicObject">3. Object, Kernel, BasicObject</a>
Następnym miejscem w którym szuka Ruby jest klasa nadrzędna. Tak naprawdę nawet klasa, która jawnie nie dziedziczy z żadnej klasy dziedziczy z klasy Object.
  Natomiast klasa object dzidziczyz klasy BasicObject.
  Między nimi znajduję się jeszcze moduł kernel
  
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
-->
  
### <a name="parentClass">4. Parent Class</a>
If Ruby did not find a method in a given class, it will check whether any of the parent classes from which the class inherits does not have a method with the given name.

``` Ruby
class Animal
  def me
    'Run in Parent Class'
  end
end

class Dog < Animal
end

dog = Dog.new
dog.me # => "Method from parent class"
```

### <a name="includeModules">5. Include Modules</a>
W jeżyku Ruby występuje tylko pojedyncze dziedziczenie ale dzięki modułom możemy zmieniać zachowanie klas tak jakby wielokrotne dziedziczenie było możliwe.
Za pomocą include możemy dołączać moduły tak samo jak w przypadku prepend. Jedyną róznicą jest to, że zostaą wyszukane dopiero wtedy kiedy metoda o takiej samej nazwie nie została zdefiowana w jako metoda instancji

``` Ruby
module Able
  def me
    'Able module'
  end
end

class Dog
  include Able
end

dog = Dog.new
dog.me # => 'Method from Observable module'
```

### <a name="instanceMethods">6. Instance Methods</a>
Jeśli nie stworzyliśmy żadnych metod instancji oraz nie dołączyliśmy żadnych modułów to zostanie uruchomiona metoda, która została zdefiniowana w klasie. Najczęściej metody są uruchamiane właśnie z tego miejsca.
``` Ruby
class Dog
  def me
  end
end

dog = Dog.new
dog.me # => 'Instance Method'
```

### <a name="prependModules">7. Prepend Modules</a>
Ruby nie wspiera wielokrotnego dziedziczenia ale umożliwa to za pomocą modułów. Popularnie zwanych jako mixiny. Za pomocą metody prepend możemy dołączać moduły do klas i korzystać z nich tak jakby były wbudowane.

``` Ruby
module Able
  def me
    'Able module'
  end
end

class Dog
  prepend Able
end

dog = Dog.new
dog.me # => 'Bark from Other module'
```

### <a name="singletonMethods">8. Singleton Methods</a>
Metody instancji to pierwsze miejsce, gdzie Ruby szuka danej metody. Czym jest metoda instancji? Jest to metoda, która została utworzona tylko i wyłącznie dla jendej instancji danej klasy.

``` Ruby
class Dog
end

dog = Dog.new
dog.me # => NoMethodError
  
def dog.me
  'Singleton Methods'
end
```

### <a name="super">Super</a>
### <a name="extendModules">Extend Modules</a>
### <a name="classMethods">Class Methods</a>
