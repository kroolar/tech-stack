### Singleton

#### Opis
Singleton jest kreacyjnym wzorcem projektowym, który pozwala na utworzenie tylko jednej instancji danej klasy oraz zapewnia do niej globalny dostęp.

#### Przykład
Nasza aplikacja posiada obiekt **Console**, który pozwala na wyświetlanie danych twojego kodu w konsoli.

#### Rozwiązanie

``` Ruby
class Console
  @@instance = new
  
  def self.instance
    @@instance
  end
  
  def error(text)
    raise test
  end
  
  def log(text)
    puts text
  end
  
  private_class_method :new
end

console = Console.new # => NoMethodError

console = Console.instance
console.log('Hello World!') # => Hello World

console == Console.instance # => true
```

``` Ruby
class Console
  include Singleton
  
  def error(text)
    raise test
  end
  
  def log(text)
    puts text
  end
end
```

#### Wady i Zalety
Zalety:
- Masz pewność, że istnieję tylko jedna instancja danej klasy w całej aplikacji
- Obiekt jest tworzony dopiero przy pierwszym użyciu
- Globalny dostęp do danego obiektu

Wady:
- W wielowątkowym środowisku może pojawić się więcej niż jeden obiekt
- Może to prowadzić do sytuacji, że obiekt wie zbyt dużo o innych obiektach
