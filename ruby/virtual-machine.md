# Virtual Machine
Ruby implementaions MRI YARV jruby
1. [YARV](#yarv)
2. [Interpreter](#interpreter)
3. [Interprete]
4. How Ruby Interprets code
  1. Code
  2. Tokenize
  3. AST
  4. Execute 
5. [Tokenizing](#tokenizing)
6. [Lexing](#lexing)
7. [Parsing](#parsing)
8. Garbage Collector

### <a name="yarv">1. YARV</a>
YARV(Yet another Ruby VM)


### <a name="tokenizing">2. Interpreter</a>
Zanim Ruby interpreter uruchomi program musi ztokenizować kod. Czyli  łamie fo na kawałki.
Standardowa biblioteka provide moduł Ripper, który pokazuje jak działa interpreter Rubiego, któ©a zwraca nam tablice tokenóœ.

``` Ruby
require 'ripper'

code = "x = 2 + 3"

Ripper.tokenize(code) # => ["x", " ", "=", " ", "2", " ", "+", " ", "3"] 
```

Tokenizer działa nawet jak wpiszesz coś idiotycznego

``` Ruby
code = "const a = 1,,0"
Ripper.tokenize(code) # =>
```
<br>

### <a name="#">3. Lexing</a>
### <a name="parsing">4. Parsing</a>
Ruby zmienia tezt na coś co się nazywa abstract syntaxt tree (AST) Co to jest?

### <a name="parsing">5. Compiling</a>
Cpmpiling into bytecode

Ruby kompiluje AST na kod bitowy niższego rzędu, który nastęþnie jest uruchamiany przez maszyne wirtualną Rubiego

Możemy zajrzeć do wnętrze masyny wirtualnej za pomocą
``` Ruby
RubyVM::InstructionSequence.compile('').disassemble

Następnie maszyna wirtualna (YARV) step trough these instructions executes them
```

2. Tokenization and parsing
3. Compilation
4. How ruby executes code


### Tokenization
How many times Ruby reads and transform code before running it? 3
Za każdy razem po tym jak uruchomisz ruyb w konsoli a zobaczysz wyjście kod jest czytane 3 razy

Ruby Code => Tokenize(tokens) => Parse(AST nodes) => Compile => YARV Instructions

Na początku Ruby czyta kod i zamienia go na tokeny

``` Ruby
3.times { |n| puts n } 
```

ruby test.rb # =>

Najpierw czyta całość, a potem to tokenizuje
``` Ruby
 \/
| 3 | . | t | i | m | e | s |
```

Tokenizuje to znaczy, że zamienia je na na serie tokenów czyli słów które rozumie
Widzi, że to jest jedynka i leci dalej


``` Ruby
     \/
| 3 | . | t | i | m | e | s |
```


Potem znajduje kropke i leci dalej bo może do być floating number

``` Ruby
          \/
| 3 | . | t | i | m | e | s |
```

W tym momencie RUby przerywa iteracje ponieważ orientuje się, że kropka jest częśćią oddzielnego tokena i wraca do tyłu oraz konwertuje liczbę na token tINTEGER


``` Ruby
              \/
tINTEGER(10) | . | t | i | m | e | s |
```

``` Ruby
                    \/
[tINTEGER(10)] [.] | t | i | m | e | s |
```
``` Ruby
                    \/
[tINTEGER(10)] [.] [tIDENTIFIER]
```



