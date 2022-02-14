# Terminal

### Typy elementów

| Znak | Opis                   |
|------| -----------------------|
| -    | Zwykły plik            |
| b    | Specjalny znak blokowy |
| c    | Specjalny plik znakowy |
| d    | Katalog                |
| l    | Dowiązanie symboliczne |
| p    | Nazwany potok          |
| s    | Gniazdo                |

### Prawa dostępu
użytkownik-grupa-inni

| Znak | Opis dla katalogów         | Opis dla plików |
|------|----------------------------|-----------------|
| r    | Do przeszukania zawartości | Do odczytywania |
| w    | Do zmiany zawartości       | Do modyfikacji  |
| x    | Do wejścia do katalogu     | Do uruchamiania |

Przechodzenie między katalogami

cd
cd ~
cd /
cd ..

Tworzenie nowego katalogu

```
$ mkdir katalog
```

Z prawami
mkdir -m 111 kat

Z opisem
-v, --verbose

Usuwanie
rmdir

rmdir --verbose

rm -R

Tworzeni plików touch

Usuwanie plików
rm
-r, -R --recursive

-f, --force

pyta o usuniecie

-v, --verbose

Wyswietlanie zawartosci pliku

cat plik1 plik2 

touch-a zmienia czas dostatniego dostepu

Kopiowanie
cp plik1 katalog
z inna nazwa 
cp plik1 katalog/plik2

PRzenoszenie i zmiana nazwy
mv

### Nadawanie praw dostepu
```
$ chmod 777 nazwa_elementu
```

4 - r
2 - w
1 - x

Bit lepkości
Nadanie takiego bitu skutkuje tym, że tylko właściciel pliku oraz root mogą go usunać

chmod +t nazwa

chmod -t nazwa

drwxrwxr-t

passwd
zmiana hasła

passwd username

Zmiana powłoki terminala:

```
$ sh
$ bash 
```

informacje o typie pliku *

zminaa wlasciciela grupy

chwob wlasciciel:grupa plik

Wyszukiwanie 
find ./ -name 'p*'
-depth

Ile miejsca zajume element

du plik

Przełączanie na inne konto: 
```
$ su root
```

| POLECENIE           | OPIS |
|---------------------|------|
| w                   | Wyświetla kto jest obecnie zalogowany |
| free                | Wyświetla zużycie pamięci operacyjnej   |
| cal                 | Wyświetla kalendarz |
| date                | Wyświetla aktualną date |
| last                | Wyświetla ostatnio zalogowanych użytkowników |
| user, who           | Wyświetla aktualnie zalogowanych użytkowników |
| whoami              | Wyświetla informacje o użytkowniku |
| hostname            | Wyświetla nazwe hosta |
| ifconfig            | Wyświetla parametru interfejsu sieciowego |
| host _adres_strony_ | Wyświetla adres ip podanej strony |
| ping _adres_strony_ | Sprawdza czy domena odpowiada |
| uptime              | Wyświetla czas od uruchomienia strony |
| uname -a            | Wyświetla informacje o sprzęcie |
| type _polecenie_    | Wyświetla typ polecenia |
| which _polecenie_   | Wyświetla lokalizacje pliku |
| help _polecenie_    | Wyświetla pomoc dla poleceń wbudowanych w powłoke |
| man _polecenie_     | Wyświetla podręcznik programu |
| whatis _polecenie_  | Wyświetla jednowierwszowy opis polecenia |
| exit                | Kończy sesje |
| df                  | Wyświetla dostępne miejsce na dysku |
| alias               | Wyświetla aktualnie zdefiniowane aliasy |
| history             | Wyświetla historie ostatnich poleceń |
| head _nazwa_pliku_  | Domyślnie wyświetla pierwsze 10 linii tekstu |
| tail _nazwa_pliku_  | Domyślnie wyświetla ostatnie 10 linii tekstu |
| pwd                 | Wyświetla aktualną ścieżke |
| clear               | Czyści konsole |
| less                | Program do wyświetlania zawartośći pliku

Często używane opcje
-h
-i

Co to jest linux?
Co to jest powłoka?
Co robi terminal? Udsotępnia powłoke w GUI

Wirtualne konsole

Nawigacja
Hierarchia jest inna niż w windows gdzie każdy dysk ma swoją nazwe tu jest jeden root

roo directory
pwd working directory
home directory there were we can save files kazdy użytkownik go dostaje

ls zawartość katalogu

cd zmiana katalogu roboczego
bezwgledne

cd /usr/bin zaczyna się od katalogu głównego

wzgledna liczona od biezącego katalogu

Uzywa się . któ©a oznacza vieżacy katalog lub .. który oznacza katalog nadrzedny. Możemy pominąć . bo jest ona domyśłnie dodawana

nazwy
od kropki ukryte pliki ls ich nie wyisze ls -a

cd katalog domowy

cd - poprzedni katalog roboczy

cd ~artur zmienia na katalog domowy użytkownika jakiegos tam

Przegląd systemu

ls
ls -l więcej informacji

polecenie -opcje argumenty

krótkie opcje długie opcje

Nazwy plików w linuxie nie muszą odzwierciedlac typu pliku.

File pokazuje krótki opis zawartości pliku

Dowiązania symboliczne i twarde?

sudo -s przełącza na roota

Wirtualne konsoeltki

### Manipulowanie plikami i katalogami

mkdir tworzenie folderów

cp -r --recursive kopiuje katalogi i ich zawatość

mv zmiana nazwy albo przenoszenie

rm usuwanie

Możemy dodawać średnik między poleceniami

BIOS?
UEFI?
GNOME
bash
linux@linux $ - znak zachet

Dyski i partycje
Kanały IDE?
hda - pierwszy kontroler IDE, Master
hdb - pierwszy kontroler IDE, Slave
hdc - drugi kontroler IDE, Master
hdd - drugi kontroler IDE, Slave

Jeśłi ustawimy więcej partycji
hda1
hda2

Kanały SCSI?
sda
...

[admin@linux /]$ - uzytkownik@host znak zachęty($ - zwyczajny, # - root) / - katalog bieżący

W

ADministrowanie systemu
wysiwtlanie informacji o dzilajacych uslugach

dodawanie uzytkownikow
adduser nazwa

dodawaniae gtup

groupadd

procesy dzialajace 
top

echo

ssh

statystyki
stat plik.txt

grep 12 plik.txt



0. Overview
Wszystko jest plikiem, nawet urządzenia
Nie określamy rozszerzeń tylko nagłówki MIME

1. Czym jest powłoka?

Konsole wirtualne działają w tle
Ctrl+Alt+F1 - F6
PRzełączanie Alt i np. F5
ALT + F7 wyjscie

2. Nawigacja

Bieżący katalog roboczy
znak zahęty $, #
pwd, ls, cd

ściżka względna 
ściezak bezwzgędna /
folder uzytkownika ~, ~name

3. Przegląd systemu

### Wyświetlanie zawartośći katalogu
```
$ ls
```

| OPCJA | DŁUGA OPCJA      | OPIS                                                                                                        |
|-------|------------------|-------------------------------------------------------------------------------------------------------------|
| -a    | --all            | Wypisuje wszystkie elementy(nawet te ukryte)                                                                |
| -A    | --almost-all     | Działa podobnie jak powyższa opcja ale nie wyświetla bieżącego katalogu (.), ani katalogu nadrzędnego (..)  |
| -l    |                  | Wyświetla listę w długim formacie                                                                           |
| -R    | --recursive      | Wyświetla wszystkie katalogi i podkatalogi                                                                  |
| -r    | --reverse        | Wyświetla listę w odwrotnej kolejności                                                                      |
| -S    | --sort=size      | Sortuje listę na podstawie rozmiaru plików                                                                  |
| -t    | --sort=time      | Sortuje listę na podstawie czasu modyfikacji                                                                |
| -U    | --sort=none      | Nie sortuje listy                                                                                           |

Pomija elementy pasujące do danego wzorca. W tym przypadku wszystkie elementy zaczynające się na literę "p":
``` console
ls -I "p*"
ls --ignore="p*"
```

Pokazuje wszystkie katalogi pasujące do danego wzorca. W tym przypadku pokazuję wszystkie elementy rozpoczynające się na literę "D":

``` console
ls D*
```

### Szczegółowe informacje  elementach
``` console
$ ls -l
$ drwxr-xr-x 2 user user 4096 Feb 9 10:26 Desktop
```

| Kolumna | Wartość     | Opis                         |
|---------|-------------|------------------------------|
| 1       | drwxr-xr-x  | Typ elementu i prawa dostępu |
| 2       | 2           | Liczba dowiązań              |
| 3       | user        | Nazwa właściciela            |
| 4       | user        | Nazwa grupy                  |
| 5       | 4096        | Rozmiar elementu w bajtach   |
| 6       | Feb 9 10:26 | Data ostatniej modyfikacji   |
| 7       | Desktop     | Nazwa elementu               |

### Struktura katalogów:

| Katalog       | Opis                                                                                   |
| ------------- | ---------------------------------------------------------------------------------------|
| /             | Katalog główny                                                                         |
| /bin          | Pliki binarne(programy)                                                                |
| /boot         | Jądro linuksa oraz program rozruchowy                                                  |
| /dev          | Węzły urządzeń                                                                         |
| /etc          | Pliki konfiguracyjne                                                                   |
| /home         | Katalogi główne użytkowników                                                           |
| /lib          | Biblioteki używane przez programy                                                      |
| /lost + found | Wykorzystywanyy w przypadku częściowego po uszkodzeniu pliku                           |
| /media        | Punkty montowanie nośników wymiennych zamontowanych automatycznie                      |
| /mnt          | Punkty montowanie nośników wymiennych zamontowanych ręcznie                            |
| /opt          | Opcjonalne oprogramowanie                                                              |
| /proc         | Wirtualny system, który pozwala uzyskać informacje o systemie                          |
| /root         | Katalog domowy głównego użytkownika                                                    |
| /sbin         | Specjalne pliki binarne(programy) do uzytku głównie dla użytkownia uprzywilejowanego   |
| /tmp          | Pliki tymczasowe                                                                       |
| /usr          | Programy wykorzystywane przez użytkowników                                             |
| /var          | Miejsce przechowywanie dynamicznych danych tj. bazy danych, pliki kolejek, poczta itp. |


### Wieloznaczniki:

| Wieloznacznik | Znaczenie                                                            |
| ------------- | -------------------------------------------------------------------- |
| *             | Pasuje do dowolnych _znaków_                                         |
| ?             | Pasuje do dowolnego pojedynczego _znaku_                             |
| [znaki]       | Pasuje do dowolnegowchodzącego w skład zestawu _znaki_               |
| [!znaki]      | Pasuje do dowolnego znaku, który nie wchodzi w skład zestawu _znaki_ |
| [[:klasa:]]   | Pasuje do dowolnego znaku wchodzącego w skład określonej _klasy_     |


### Klasy znaczników

| Znacznik  | Znaczenie                                  |
|-----------|--------------------------------------------|
| [:alnum:] | Pasuje do dowolnego znaku alfanumerycznego |
| [:alpha:] | Pasuje do dowolnego znaku alfabetycznego   |
| [:digit:] | Pasuje do dowolnej liczby                  |
| [:lower:] | Pasuje do dowolnej małej litery            |
| [:upper:] | Pasuje do dowolnej wielkiej litery         |


### Tworzenie katalogów:

```
$ mkdir nazwa_katalogu
```

### Kopiowanie

```
$ cp element1 element2
```

### Przenoszenie plików lub zmiana nazwy

```
$ mv element1 element2
```

### Usuwanie elementów

Usuwanie plików:
```
rm plik
```

Usuwanie katalogów:
```
rm -r katalog
```

5. Polecenia

### Czym są polecenia?
- Programem wykonywalnym
- Poleceniem wbudowanym
- Funkcją powłoki
- Aliasem

# 10. Procesy
Proces jest poleceniem lub programem wykonującym się na komputerze. Procesy często są programami, które nie posiadają interfejsu graficznego i są wykonwyane w tle.

### Wyswietlanie procesów
Poniższa komenda wyświetla tylko procesy wykonywane w aktualnej sesji terminala.
```
$ ps
```

Jeśli chcemy wyświetlić wszystkie procesy musimy przekazać argument _x_ do plecenia _ps_.
```
$ ps x
```

Możemy także wyświetlić procesy w postaci drzewa.
```
$ pstree
```

### Oznaczenie procesu
Po wyświetleniu procesów w kolumnie STAT wyświetli nam sie litera, która odpowiada za jego oznaczenie.

| STATUS | OPIS                                                         |
|--------|--------------------------------------------------------------|
| R      | Proces jest uruchomiony lub gotowy do uruchomienia           |
| S      | Uśpiony                                                      |
| D      | Uśpiony nieprzerywalny                                       |
| T      | Zatrzymany.                                                  |
| Z      | Proces "Zombie". Zakończył działanie ale nie został usunięty |
| <      | Proces o wysokim priorytecie                                 |
| N      | Proces o niskim priorytecie                                  |

### Dynamiczne wyświetlanie procesów.
Polecenie _top_ pokazuje procesy, które najbardziej obciążają nasz komputer. Polecenie to odświeża swój stan co 3 sekundy.
```
$ top
```

### xlogo
xlogo to program, który po porstu wyświetla literę _x_ w graficznym oknie. Wykorzystamy ten przykład, żeby uruchomić przykładowy proces.
```
$ xlogo
```

W tym momencie z terminala zniknął nam znak zachęty.

### Zatrzymanie procesu
Jeśli chcemy zatrzymać aktualny proces możemy naciśnąć kombinacje klawiszy _Ctrl + C_.

### Umieszczanie procesu w wtle
W tym przykładzie uruchomimy program xlogo w tle za pomocą argumentu _&_.
```
$ xlogo &
```

Terminal zwróci jego identyfikator PID(Process ID), a znak zachęty dalej będzie dostępny. Wpisując _ps_ możemy sprawdzić, że proces nadal działa.

# Wyświetlanie zadań uruchomionych z poziomu naszego terminala
Jeśli chcemy sprawdzić procesu uruchomione z poziomu naszego terminala możemy to zrobić za pmocą komendy _jobs_.
```
$ jobs
```

Po wpisaniu tej komendy powinien się wyświetlić tylko proces _xlogo_.

### Przywrócenie procesu
Jeśli chcemy, żeby proces znowu zaczął działac w konsoli musimy użyć komendy _fg_ wraz z argumentem w postaci _%_ oraz numery zadania. Jeśli istnieje tylko jedno zadanie nie trzeba podawać żadnego argumentu.
```
$ fg %1
$ fg
```

### Przeniesienie procesu do pracy w tle
Jeśli spowrotem chcemy przerzucić proces do pracy w tle możemy skorzystać z polecenia _gb_, które działa podobnie jak polecenie _fg_.
```
$ gb %1
$ gb
```

### Sygnały
Polecenie nie zabija procesu automatycznie, tylko wysyła sygnał, który ysprawdza czy proces odpowiada i pozwala mu się przygotować na zamknięcie. _Ctrl + C_ jest w rzeczywistości sygnałem _INT_.

```
$ kill PID
```

### Oznaczenie sygnałów

| NUMER | NAZWA | OPIS                                                                                                                    |
|-------|-------|-------------------------------------------------------------------------------------------------------------------------|
| 1     | HUP   | _Hung up_. Sygnał ten ejst wykorzystywany do ponownej inicjalizacji                                                     |
| 2     | INT   | _Interrupt_. Zwykle Zatrzymuje działanie programu. Działa jak _Ctrl + C_                                                |
| 9     | KILL  | _Kill_. Sygnał ten nie jest wysyłany do programu. Jądro linuksa natychmiastowo kończy działanie procesu.                |
| 15    | TERM  | _Terminate_. Domyślny sygnał wysyłany przez polecenie. Jeśli proces jest wystarczajac żywy to zakończy swoje działanie. |
| 18    | CONT  | _Continue_. Sygnał ten wznawia proces zatrzymany przez sygnał _STOP_.                                                   |
| 19    | STOP  | _Stop_. Proces zatrzymuje działanie ale go nie kończy.                                                                  |

### Wyłączanie systemu
Istnieje kilka poleceń, które pozwalają na przerwanie pracy systemu

| POLECENIE | OPIS                                                     |
|-----------|----------------------------------------------------------|
| halt      | Wstrzymuje działanie systemu. Działa jak opcja _wyloguj_ |
| poweroff  | Wyłącza system                                           |
| reboot    | Uruchamiania pownownie system                            |

Istnieje jeszcze polecenie _shutdown_, które pozwala wykonań jedno z powyższych poleceń i na dodatek można do niego przekazać argument, który określi czas wykonania tego polecenia.
```


