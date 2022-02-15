# Procesy
Proces jest poleceniem lub programem wykonującym się na komputerze. Procesy często są programami, które nie posiadają interfejsu graficznego i są wykonwyane w tle.

- [Wyswietlanie procesów](#one)
- [Oznaczenie procesu](#two)
- [Dynamiczne wyświetlanie procesów](#three)
- [xlogo](#four)
- [Zatrzymanie procesu](#five)
- [Umieszczanie procesu w tle](#six)
- [Wyświetlanie zadań uruchomionych z poziomu naszego terminala](#seven)
- [Przywrócenie procesu](#eight)
- [Przeniesienie procesu do pracy w tle](#nine)
- [Sygnały](#ten)
- [Oznaczenie sygnałów](#eleven)
- [Wyłączanie systemu](#twelve)

### <a name="one">Wyswietlanie procesów</a>
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

### <a name="two">Oznaczenie procesu</a>
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

### <a name="three">Dynamiczne wyświetlanie procesów</a>
Polecenie _top_ pokazuje procesy, które najbardziej obciążają nasz komputer. Polecenie to odświeża swój stan co 3 sekundy.
```
$ top
```

### <a name="four">xlogo</a>
xlogo to program, który po porstu wyświetla literę _x_ w graficznym oknie. Wykorzystamy ten przykład, żeby uruchomić przykładowy proces.
```
$ xlogo
```

W tym momencie z terminala zniknął nam znak zachęty.

### <a name="five">Zatrzymanie procesu</a>
Jeśli chcemy zatrzymać aktualny proces możemy naciśnąć kombinacje klawiszy _Ctrl + C_.

### <a name="six">Umieszczanie procesu w tle</a>
W tym przykładzie uruchomimy program xlogo w tle za pomocą argumentu _&_.
```
$ xlogo &
```

Terminal zwróci jego identyfikator PID(Process ID), a znak zachęty dalej będzie dostępny. Wpisując _ps_ możemy sprawdzić, że proces nadal działa.

### <a name="seven">Wyświetlanie zadań uruchomionych z poziomu naszego terminala</a>
Jeśli chcemy sprawdzić procesu uruchomione z poziomu naszego terminala możemy to zrobić za pmocą komendy _jobs_.
```
$ jobs
```

Po wpisaniu tej komendy powinien się wyświetlić tylko proces _xlogo_.

### <a name="eight">Przywrócenie procesu</a>
Jeśli chcemy, żeby proces znowu zaczął działac w konsoli musimy użyć komendy _fg_ wraz z argumentem w postaci _%_ oraz numery zadania. Jeśli istnieje tylko jedno zadanie nie trzeba podawać żadnego argumentu.
```
$ fg %1
$ fg
```

### <a name="nine">Przeniesienie procesu do pracy w tle</a>
Jeśli spowrotem chcemy przerzucić proces do pracy w tle możemy skorzystać z polecenia _gb_, które działa podobnie jak polecenie _fg_.
```
$ gb %1
$ gb
```

### <a name="ten">Sygnały</a>
Polecenie nie zabija procesu automatycznie, tylko wysyła sygnał, który ysprawdza czy proces odpowiada i pozwala mu się przygotować na zamknięcie. _Ctrl + C_ jest w rzeczywistości sygnałem _INT_.
```
$ kill PID
```

### <a name="eleven">Oznaczenie sygnałów</a>

| NUMER | NAZWA | OPIS                                                                                                                    |
|-------|-------|-------------------------------------------------------------------------------------------------------------------------|
| 1     | HUP   | _Hung up_. Sygnał ten ejst wykorzystywany do ponownej inicjalizacji                                                     |
| 2     | INT   | _Interrupt_. Zwykle Zatrzymuje działanie programu. Działa jak _Ctrl + C_                                                |
| 9     | KILL  | _Kill_. Sygnał ten nie jest wysyłany do programu. Jądro linuksa natychmiastowo kończy działanie procesu.                |
| 15    | TERM  | _Terminate_. Domyślny sygnał wysyłany przez polecenie. Jeśli proces jest wystarczajac żywy to zakończy swoje działanie. |
| 18    | CONT  | _Continue_. Sygnał ten wznawia proces zatrzymany przez sygnał _STOP_.                                                   |
| 19    | STOP  | _Stop_. Proces zatrzymuje działanie ale go nie kończy.                                                                  |

### <a name="twelve">Wyłączanie systemu</a>
Istnieje kilka poleceń, które pozwalają na przerwanie pracy systemu

| POLECENIE | OPIS                                                     |
|-----------|----------------------------------------------------------|
| halt      | Wstrzymuje działanie systemu. Działa jak opcja _wyloguj_ |
| poweroff  | Wyłącza system                                           |
| reboot    | Uruchamiania pownownie system                            |

Istnieje jeszcze polecenie _shutdown_, które pozwala wykonań jedno z powyższych poleceń i na dodatek można do niego przekazać argument, który określi czas wykonania tego polecenia.
