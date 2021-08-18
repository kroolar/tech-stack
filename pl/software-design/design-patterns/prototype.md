## Prototype

**Typ:** Kreacyjny

**Cel:** Pozwala kopiować już istniejące obiekty

### Problem
Mamy fabrykę w której produkujemy samochody. Jeśli chcemy stworzyć dwa lub więcej takich samych samochodów nie chcemy ich budować od nowa tylko skopiować wszystko i nadać nowy numer seryjny,

### Rozwiązanie
``` Ruby
class Car
  attr_reader :brand, :model, :serial_number

  def initialize(brand:, model:, serial_number:)
    @brand = brand
    @model = model
    @serial_number = serial_number
  end

  def clone(serial_number)
    Car.new(
      brand: self.brand,
      model: self.model,
      serial_number: serial_number
    )
  end
end

car = Car.new(brand: 'BMW', model: 'E36', serial_number: 1)
clone = car.clone(2)
```

### Plusy i minusy
➕ Może być alternatywą dla dziedziczenia

➕ Można pozbyć się powtarzającego kodu inicjalizacyjnego tworząc gotowe wzorce

➖ Klonowanie złożonych obiektów może okazać się trudne

### Źródła
- https://medium.com/@dljerome/design-patterns-in-ruby-prototype-342cb26ea75
- https://refactoring.guru/design-patterns/prototype
