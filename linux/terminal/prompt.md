# Znak zachęty

### Domyślny znak zachęty

```
[me@linux ~]$
```

echo $PS1

# Dostosowanie znaku zachęty
Znak zachęty zapisany jest w zmiennej _PS1_. Możemy ją sprawdzić za pomocą komendy _echo_.
```
$ echo $PS1
```

Jeśli chcemy zmodyfikować znak zachęty wystarczy, że podmienimy zmienną _$PS1_.
```
$PS1="Prompt: "
```

Aby odzyskać dawny wygląd znaku zachęty wystarczy zrestartować terminal. Jeśli chcemy podmienić znak zachęty na stałe powinniśmy podmienić zmienną _PS1_ w pliku _.bashrc_.

Modyfikujać nasz znak zachęty możemy, opróćz samego tekstu możemy zmienć także kolor, lub podać specjalny znak specjalny, który umożliwi nam wyświetlanie dodatkowych informacji. Poniżej przykład domyślnego znaku zachęty w dystrybucji Ubuntu.

```
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$
```
