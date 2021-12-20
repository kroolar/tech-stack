# Development vs Product

### Environments

Środowiskiem deweloperskim można okreslić maszyne na której odpalany jest program oraz dołączone do tej maszyny oprogramowanie oraz zbiór narzędzi. Każde Środowisko działa w innych warunkach oraz każde ma inny cel oraz funkcje. Najczęściej spotyka się 4 rodzaje środowisk:

- Development
- Test
- Staging
- Production

#### Development
Pierwsze środowisko z którym styka się deweloper. Środowisko to jest uruchamiane na lokalnym komputerze dewelopera. Środowisko to służy do codziennej pracy z rozwojem oprogramowania. Podczas pisania kodu większość rzeczy nie działa tak jak powinna dlatego środowisko to w żaden sposób nie powinno wpływać na nic poza jego obrębem.

#### Test
Kolejnym środowiskiem jest środowisko testowe. Pozwala wykonywać wcześniej napisane testy dzięki czemu możemy szybciej identyfikować błędy.

#### Staging
To środowisko powinno symulować działanie prawdziwego systemu w realnym otoczeniu. W zależności od potrzeb dostęp do niego mogą mieć deweloperzy i testerzy, którzy mogą testować końcowy produkt w przyjaznym środowisku jaki ownerzy, którym chcemy przedstawić rezultat pracy. Staging tak jak i produkcja jest uruchamiany na serwerze zewnętrznym do którego dostęp powinny mieć tylko zainteresowane osoby.

#### Production
Środowisko produkcyjne jest ostatnim środowiskiem w procesie tworzenia oprogramowania. Aplikacja trafia tam po dokładnym przetestowaniu na stagingu. Różnica między produkcją, a stagingiem jest taka, że jest najczęściej publicznie dostępna, a wszystkie zmiany są dokonywane na żywo.

### DB
W środowisku

### CloudService
Cloud albo local

### Mailer
Wysyłanie albo przechwytywanie
### Eager Load
### Exceptions
owinno pokazywać błąð
### Caching

### Server
### Webpacker
### Secrets
### Data migration
