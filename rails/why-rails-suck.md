# Why Rails Suck?
Co to jest wzorzecz i antywzorzec?

### Model
- Czym jest model
- Za co jest odpowiedzialny?

Fat Model
- Asocjacje
- Metody
- Zapytania
- Scope
- Walidacje
- - Callbacks


### View
Głównym zadaniem widoków w każdej aplikacji jest wyświetlanie warstwy prezentacji.
Widok powinien zajmować się wyświetlaniem danych, grafiki, linków, fomrularzy itp.

Action View pozwala nam natomiast na wstawienie dowolnego kodu Ruby do plików widoku.
Możemy dodawać logikę, zapytania, wyrażenia warunkowe itp. Co nie powinno mieć miejsca

``` erb
<% if current_user.admin? %>
  <ul>
    <% User.where(role: 'developer').map do |user| %>
      <li>Name: <%= "#{user.first_name} #{user.last_name}" %></li>

      <% if user.team.present? %>
        <li>Team: <%= "#{user.team.name}" %></li>
      <% end %>

      <li>Manager: <%= "#{user.team.manager.name}" %></li>
    <% end %>
  </ul>
<% end %>
```

Nawet jeśli zawiera tylko dane do wyświetlenia to zaburza całą strukture przez co całość staję się nieczytelna
ciężko ją utrzymać, porpawić i testować.

Action View pozwala nam korzystać z pewnych narzędzi takich jak helpery, partials, możemy skorzystać ze wzorców takich
jak fasada i dekorator, aby lepiej tworzyć widoki.

I to kiedyś wystarczało ale w dzisiejszych czasach tworzymy coraz bardziej złożone systemy, przez co warstwa prezentacji staję się coraz bardziej złożona.

Warstwa prezentacji sama w sobie jest przeważnie budowana z kilku technologi tj. HTML, CSS, JS i mnóstwa innych dodatkowych narzędzi więc mieszanie jej z Rubim jeszcze bardziej ją utrudnia.
Tak naprawdę to nie jest tylko wyświetlanie danych ale także obsługa formularzy, odbieranie i wysyłanie danych, walidowanie, animacje, semantyka itp.

Widok powinien być tak prosty, żeby programista, który nie zna Rubiego mógł swobodnie pracować z takim plikiem.

Jak używać widoków w Rails, żeby się dobrze z nimi pracowało. Nie używać!

Tak naprawdę warstwa prezentacji powinna zostać zastąpiona warstwą klienta, które de facto jest osboną aplikacją.

Railsy pozwalają na tworzenie aplikacji only-api, która nie posiada widoków.
Wystarczy użyć gotowych narzędzi jak Gatsby, NextJS lub Create React App do stworzenia aplikacji, która
pozwoli na odłączenie warstwy klienckiej od warstwy serwerowej

Zalety:
- Łatwiej testować pojedyncze moduły
- Łatwiejsze w zrozumieniu i zarządzaniu(wystarczy znać jeden kontekst)
- Zespoły mogą pracować prawie niezależnie od siebie
- Łatwiej dodawać i wdrażać nowe funkcjonalności, które są niezależne od częśći serwerowej

Wady:
- Więcej konfiguracji(API, sesje, cache)
- Trudniej testować całą aplikację
- Mniejsze bezpieczeństwo
- Mniejsza niezawodność
- Komunikacja między modułami jest wolniejsza

Kiedy stosować?
- Jeśli aplikacja zaczyna się rozrastać

### Controller
Kontrolery odpowiadają za odbieranie i obsługę żądań. Jest także mostem, kßóry łąćzy model i widok
- Uwierzytelnianie i autoryzację
sprawdzenie czy podmiot jest tym za kogo się podaje, sprawdzenie czy ma dosteþ do zasobów lub wykoannia akcji
- Pobieranie potrzebnych danych
- Template rendering
- powinien zwrócić jakiś resultat w dobrym formacie (HTML, JSON) albo przekierować do innej ścieżki
- Umieszczenie logiki biznesowej

Najsłynniejszym jestr Fat Controller

Problemy
QueryObject
ServiceObject

- A repeated pattern of action, process, or structure that initially appears to be beneficial but ultimately produces more bad consequences than beneficial results
- A refactored solution that is clearly documented, proven in actual practice, and
repeatable

- Powtarzający się wzór działania, procesu lub struktury, który początkowo wydaje się być korzystny, ale ostatecznie powoduje więcej złych konsekwencji niż korzystnych wyników
- Zrefaktoryzowane rozwiązanie, które jest jasno udokumentowane, sprawdzone w praktyce i powtarzalny

Railsy posiadają generatory są dynamiczne i pozwalają szybko budować aplikację, przez co może ona trochę stracić na jakości

Model
Resposibilities
- Callbacks
- Associations
- Methods
- Scopes
- Validations
- Queries

Law of demeter
``` Ruby
class Employee < ActiveRecord::Base
  belongs_to :user
end

class User < ActiveRecord::Base
  has_one :employee
end

@user.employee.name
@user.employee.address

class User < ActiveRecord::Base
  has_one :employee
  
  def name
    employee.name
  end
  
  def address
    employee_address
  end
end

@employee.name
@employee.address

class User < ActiveRecord::Base
  has_one :employee
  
  delegate :name, :address, to: employee
end

@employee.name
@employee.address

class User < ActiveRecord::Base
  has_one :employee
  Controllers put the C in MVC and are a fundamental part of the Rails framework.
However, the relationship that many Rails programmers have with controllers is
 complex.
On one hand, controllers are categorically
  delegate :name, :address, to: employee, prefix: true
end

@employee.employee_name
@employee.employee_address
```
https://apidock.com/rails/Module/delegate

### Controller
### AntiPattern: Homemade Keys
Problem
Solution: Devise

### AntiPattern: Fat Controller
Jest jednym z najczęściej występujących antywzorców. Ale również jednym z łatwiejszych do naprawienia.
Najczęśćiej mamy tam logikę biznesową i zapytania, które powinny należeć do modelu
