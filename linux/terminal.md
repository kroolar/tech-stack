# Terminal

### Wyświetlanie zawartośći katalogu

```console
ls
dir
```

Szczegółowe informacje o katalogu:

``` console
ls -l
vdir
```

Wyświetla wszystkie pliki i katalogi(nawet te ukryte):

``` console
ls -a
```

Podobnie jak powyższa komenda wyświetla wszystkie pliki i katalogi ale dodatkowo pomija katalog bieżący(.) i nadrzędny(..):

``` console
ls -A
```

Pomija wyświetlanie kopii zapasowych:

``` console
ls -B
```

Pomija elementy pasujące do danego wzorca. W tym przypadku wszystkie elementy zaczynające się na literę "p":

``` console
ls -I "p*"
ls --ignore="p*"
```

Pokazuje wszystkie katalogi pasujące do danego wzorca. W tym przypadku pokazuję wszystkie elementy rozpoczynające się na literę "D":

``` console
ls D*
```

Pokazuje wszystkie katalogi i podkatalogi:

``` console
ls -R
ls --recursive
```

Odwraca kolejność zwracanej listy:

``` console
ls -r
ls --reverse
```

Sortuje według wielkości pliku:

``` console
ls -S
ls --sort=size
```

Sortuje według czasu utworzenia:

``` console
ls -t
ls --sort=time
```

Pomija sortowanie:

``` console
ls -U
ls --sort=none
```

### Szczegółowe informacje  elementach
``` console
$ ls -l
$ drwxr-xr-x 2 user user 4096 Feb 9 10:26 Desktop
```

Znaczenie poszczególnych kolumn:
1. Typ elementu i prawa dostępu(drwxr-xr-x)
2. Liczba powiązań(2)
3. Właściciel(user)
4. Grupa przypisana do elementu(user)
5. Rozmiar elementu (4096)
6. Data modyfikacji (Feb 9 10:26)
7. Nazwa elementu (Desktop)

Typy elementów
- - zwykły plik
b - specjalny znak blokowy
c - specjalny plik znakowy
d - katalog
l - dowiązanie symboliczne
p - nazwany potok
s - gniazdo

Prawa dostępu
użytkownik-grupa-inni
dal katalogów
r = do przeszukania zawartości
w - do zmiany zawartości
x - do wejścia do katalogu

Dla plików
r - do odczytywania pliku
w - do modyfikacji pliku
x - do uruchamiania pliku

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

Nadawanie praw dostepu

chmod 777 nazwa
4 - r
2 - w
1 - x

Bit lepkości
Nadanie takiego bitu skutkuje tym, że tylko właściciel pliku oraz root mogą go usunać

chmod +t nazwa

chmod -t nazwa

drwxrwxr-t

alias
pokazuje aliasy

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

Informacje o ilości wolnego miejsca
df

Ile miejsca zajume element

du plik
more i less edytory

czyszcenie clear

Sprawdzenie aktualnej ścieżki:

```
$ pwd
```

Przełączanie na inne konto: 

```
$ su root
```

Informacje o sprzęcie:

```
$ uname -a
$ uname --all
```

kto jest obecnie zalogowany
w

pamiec systemowa
free

cal

date

last ostatnio zalogowani uzytkownicy

who kto jest aktualnie zalogwany
users, who

informacja o nszym loginie who am i, whoami

nazwa hosta 
hostname

paramtery intefejsu siecowego
ifconfig

nazaw lub adrs ip
host www.helion.pl
-a

whois www.helion.pl
sprawdzenie czy dana domena jest juz alogowana

sprawdzenia dostepnosci ping helion.pl

uptime czas od uruchomienia syste,y

-i, --interactive
Co to jest linux?
Co to jest powłoka?
Co robi terminal? Udsotępnia powłoke w GUI

Wirtualne konsole

date

cal

### Free disc space
df wolne miejsce na dysku
free wolna pamięć operacyujna
exit koniec sesji

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

less progrma ktory pozwala odpalac teskty


Katalogi
/ katalog główny
/bin pliki binarne(programy) niezbędne do działania systemu
/boot Jądro linuksa oraz program rozruchowy(grub)
/dev wężly urządzeń. Wszystkie urządzenia jako pliki
/etc ogólnosystemowe pliki konfoguracyjne np. crontab
/home każdy użytkownik otrrzymuje tu swój folder
/lib biblioteki
/lost+found Jeśli nic sie nie dzieje jest pusty. Wykorzystywany do odzyskiwania plików po awariach
/media nośniki wymienne zamontowane automatycznie
/mnt nośniki wymienne zamontowane ręcznie
/opt Opcjonalene oprogramowanie
/proc Pliki które pokazują jak linuks widzi nasz komputer
/root katalog domowy głównego użytkownika(roota)
/sbin pliki binarne systemu
/tmp pliki tymczasowe tworzone przez różne programy
/usr wszystkie programy
/var miejsce przeechowywania danych, bazy danych, kolejki, poczta


Dowiązania symboliczne i twarde?

sudo -s przełącza na roota

Wszystko jest plikiem
Wirtualne konsoeltki

### Manipulowanie plikami i katalogami
### Wieloznacziki
* Pasuje do dowolych znaków
? Pasuje do dowolnego pojedynczego znaku
[znaki] Pasuje do dowolnego znaku wchodzdącego w skład zestawu znaki
[!znaki] Pasuje do dowolnego znaku który nie wchodzi w skład
[[:klasa]] Pasuje do dowolnego znaku wchodzącego w skład klasy

[:digit] Do dowolnej liczby
[:lower] Dowolna mała litera

mkdir tworzenie folderów

cp -r --recursive kopiuje katalogi i ich zawatość

mv zmiana nazwy albo przenoszenie

rm usuwanie


Czym jest polecenie
- Programem znajdującym się w katalogu usr/bin
- Poleceniem wbudowanym w samą powłoke
- Funkcją powłoki?
- Aliasem

Type pozwala sprawdzić czym jest polecenie

Which sprawdzamy gdzie jest zlokalizowany rogram


help cd
cd --help
man cd
whatis cd
info ruby

Możemy dodawać średnik między poleceniami

alias pokazuje wszystkie aliase


BIOS?
UEFI?
GNOME
bash
linux@linux $ - znak zachet

Katalogi
bin - programy dostępne dla użytkowników systemu
dev - urządzenia blokowe i znakowe
etc - pliki konfiguracyjne systemu
home - katalogi główne użytkowników
lib - pliki bibliotek dla programów
mnt - montowane dyski
proc - informacje o systemie
root - katalog użytkownika root
sbin - progamy specjalne dla użytkowników o odpowiednich uprawnieniach
tmp - pliki tymczasowe
usr - programy
var - katalog do przechowywanie potrzebnych ,u danych

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


man

Nie określamy rozszerzeń tylko nagłówki MIME

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
'history

pierwze linie tekstu
head plik.txt

ostatnie 

tail

statystyki
stat plik.txt

grep 12 plik.txt


1. Czym jest powłoka?

Powłoka to program, który pomaga się komunikować z systememe operacyjnym.

```
$ date
$ cal
```

Ilość wolnego miejsca na dysku

```
df
```

Wolna pamięć operacyjna:
```
$ free
```

Wyjście z terminala:
```
$ exit
```

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
