# Application Servers

### 1. Czym jest web server
We serwer jest odpowiedzialny za obsługe żądań między strony internetowej. W przypadku standardowej statycznej strony internetowej wszystkie jej zasoby tj. pliki html, CSS, JS oraz obrazki się nie zmieniają dlatego klient wysyła żądanie o jakiś zasób i otrzymuje go z powrotem zawsze w takim samym stanie.

### 2. Czym jest app server
Aplikacja internetowa jest bardziej złożóna. Uzytkownik może nie tylko obierać dane ale także na nie wpływać poprzez ich dodawanie, usuwanie lub modyfikacje. Serwer aplikacji jest pośrednikiem między klientem, który wysyła żądanie, a logiką biznesową(kodem), która to żadanie wykonuje, a następnie zwraca odpowiedź klientowi. Serwer aplikacji może działać bez serwera webowego, ale najczęściej znajduję się przed nim zajmując się zarządzaniem requestami i przekazywaniu ich do serwera aplikacji.

### 3. Pojęcia

#### Clustering
Cluster to grupa maszyn(computer or servers) dedykowana do jednego celu. Proces grupowania serverów nazywa się clusteringiem. W tym przypadku może to być kilka serweróœ na których zainstalowana jest ta sama aplikacja. Pojęcie to odnosi się to używania oprogramowania, które pozwala zarządzać tymi serwerami(klastrem), dzięki czemu można lepiej rozłożyć ruch co poskutkuje szybszymi odpowiedziami oraz systemem bardziej odpornym na błędy.

#### Multhithreaded
Wielowątkowość jest to funkcja, dzięki, której CPU jest w stanie uruchomić i obsługiwać więcej niż jeden wątek, korzystająć z tych samych zasób równolegle

#### Slow client buffering
Buffering jest funkcjonalnością, która pozwala na pre-laoding części danych przed ich użyciem.

#### Zero Downtime Deploy
Pojęcie to oznacza, żę aplikacja nigdy nie zostanie wyłączona ani niestabilna podczas procesu deploymentu. Aby to osiągnąć serwer musi poczekać z serwowaniem nowej wersji dopóki proces się nie zakończy.

#### ActionCable
Jest to moduł, który pozwala na integracje aplikacji Rails z WebSockets.

### 4. Serwer Railsowe
Najczęściej używanymi serwerami w aplikacjach rails są:

- Puma
- Unicorn
- Passenger

### Puma
https://github.com/puma/puma

Puma jest lekkim i szybkim serwerem. Jest domyśłnym serwerem dla aplikacji railsowej i idealny do rozpoczęcia przygody z rails od razu do użycia.  Jest wskazany do użytko zarówno do użytku na produkcji oraz developmencie

#### Unicorn

#### Passenger
W porównaniu do resezty posiada bardziej złożoną konfiguracje co pozwla na lepsze zarządzanie serwer sczególnie w środowisku produkcjnym.


- Mongrel
- Thin

```
                         | UNICORN | PUMA | PASSENGER |
-------------------------|---------|------|-----------|
Clustering               |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Multhithreaded           |   ❌    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Slow client buffering    |   ❌    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
ActionCable              |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|-----------|
Zero-Downtime Deploys    |   ✅    |  ✅  |    ✅     |
-------------------------|---------|------|------------
```
