# Monolit
![](https://d2m6ke2px6quvq.cloudfront.net/uploads/2020/09/11/3f3de3fc-f3a8-4cd1-81cd-518496f59141.jpg)

### Zalety
- Globalna dostępność całego kodu
- Mało konfiguracji
- Łatwe debugowanie i testowanie
- Łatwe wdrażanie
- Łatwa do zbudowania
- Łatwo się w niej poruszać na początku
- Dobry dla DevOpsów i Security
- Wystarczy zarządzać jednym serwerem
- Większe bezpieczeństwo

### Wady
- Aplikacja staję się bardziej wrażliwa. Jedna zmiana może stworzyć wiele problemóœ
- Musisz znać dużo kontektstu zanim zaczniesz kodować przez co nie możesz wprowadzać nowych ludzi
- Trudno zarządzać i zrozumieć działanie aplikacji
- Trudno wprowadzać zmiany, kod oddziałowuje an inne częśći
- Trudno wprowadzać nowe technologie

### Kiedy stosować?
- W początkowej fazie projektu
- W małych i prostych aplikacjach
- Jeśli nie masz wiedzy ani doświadczenia w mikroserwisach

# Mikroserwisy
Mikroserwisy to aplikacja złożona z kilku mniejszych serwisów, najczęściej każdy z nich ma swój własny proces, bazę danych i komunikują się ze sobą za pomocą API.
Często są podzielone ze względu na cele biznesowe.

![](https://d2m6ke2px6quvq.cloudfront.net/uploads/2020/09/11/2381c271-4fde-4cc1-94d9-a2e2d72a81c0.jpg)

### Zalety
- Elastyczność w doborze technologi, każdy serwis może być zbudowany w innej technologii
- Każdy serwis można wdrażać niezależnie od pozostałych
- Błąd w jednym serwisie nie oddziałowuje na całą aplikację
- Łatwiej dodawać nowe funkcjonalności
- Łatwiejsze w zrozumieniu i zarządzaniu(wystarczy znać jeden kontekst)
- Lepsza skalowalność
- Łatwiej testować pojedyncze moduły

### Wady
- Trudniej testować całą aplikację
- Komunikacja między modułami jest wolniejsza niż w przypadku monolitu
- Mniejsza niezawodność
- Mniejsze bezpieczeństwo
- Więcej konfiguracji(bazy danych, API, logowanie, cache)

### Kiedy stosować?
- Jeśli twoja aplikacja zaczyna się rozrastać 
- Jeśli masz wiedze i doświadczenie w mikroserwisach

# Modular Monoliths
![alt text](https://cdn.shopify.com/s/files/1/0779/4361/files/MonolithvsMicroservicesbySimonBrown.jpg?v=1550774521)

### Artykuły
Dekonstrukcja monolitu: https://shopify.engineering/deconstructing-monolith-designing-software-maximizes-developer-productivity

Monolit vs Mikroserwisy: https://www.n-ix.com/microservices-vs-monolith-which-architecture-best-choice-your-business/
