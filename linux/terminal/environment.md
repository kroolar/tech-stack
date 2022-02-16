# Środowisko

Środowiskiem możemy nazwać zestaw informacji na temat sesji powłoki. Środowisko przechowywuje dwa typy danych: _zmienne środowiskowe_ oraz _zmienne powłoki_. Oprócz tego powłoka przechowuje także _aliasy_, _dane programowalne_ oraz _funkcje powłoki_.

### <a name="one">Przeglądanie środowiska</a>
Polecenie _set_ wyświetla zmienne środowiskowe, zmienne powłoki oraz funkcje powłoki.
```
$ set
```

Polecenie _prinenv_ wyświetla tylko zmienne środowiskowe.
```
$ printenv
```

Możemy wyświetlić dowolną zmienną środowiskową za pomocą polecenia _echo_ dodając przed jej nazwą znak dolara($).
```
$ echo $USER
```

Polecenie _set_ oraz _printenv_ nie wyświetlają _aliasów_. Jeśli chcemy zobaczyć _aliasy_ zdefiniowane w naszym środowisku musimy skorzystać z polecenia _alias_.
```
$ alias
```

### <a name="two">Konfiguracja środowiska</a>

Jeśli chcemy zmodyfikować konfiguracje naszej powłoki, dodać zmienne lub aliasy, możemy do zrobić modyfikująć plik _.bashrc_. Możemy to zrobić globalnie dla całego systemu albo tylko dla jednego użytkownika.

| PLIK             | OPIS                                                                                   |
|------------------|----------------------------------------------------------------------------------------|
| /etc/bash.bashrc | Globalny plik konfiguracyjny                                                           |
| ~/.bashrc        | Plik startowy użytkownika. Można go użyć do nadpisania lub rozszerzenia pliku głównego |

Zmiany w pliku _.bashrc_ nie zostaną zastosowane dopóki nie zostanie rozpoczęta nowa sesja powłoki. Dzieje się tak ponieważ powłoka odczytuje plik konfiguracyjny przy inicjalizacji. Możemy to obejść stosując polecenie _source_, które pozwoli na ponowne wczytanie konfiguracji.

```
$ source ~/.bashrc
```
