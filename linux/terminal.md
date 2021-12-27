# Terminal

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
