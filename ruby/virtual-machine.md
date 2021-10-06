# Virtual Machine
Ruby implementaions MRI YARV jruby
1. [Ruby Language](#rubyLanguage)
2. [YARV](#yarv)
3. [Garbage Collector](#gc)
4. [concurenncy and pallarelis and comparision to ruby 3.0]

ZALETY I WADY METAPROGRAMOWANIA

4. [Interpreter](#interpreter)
5. [Interprete]
6. How Ruby Interprets code
  1. Code
  2. Tokenize
  3. AST
  4. Execute 
7. [Tokenizing](#tokenizing)
8. [Lexing](#lexing)
9. [Parsing](#parsing)
10. Garbage Collector

### <a name="rubyLanguage">1. Ruby Language</a>
Ruby was invented by Yukihiro _"Matz"_ Matsumoto in 1993, and the original, standard version of Ruby is often known as Matz’s Ruby Interpreter (MRI) sometimes also called CRuby.

Over the years many alternative implementations of Ruby have been written:

* [Ruby MRI](https://github.com/ruby/ruby) - Matz's Ruby Interpreter or Ruby MRI (also called CRuby) is the reference implementation of the Ruby programming language.
* [TruffleRuby](https://github.com/oracle/truffleruby) - A high performance implementation. Built on the GraalVM by Oracle Labs.
* [JRuby](https://github.com/jruby/jruby) - The Ruby Programming Language on the JVM.
* [mruby](https://github.com/mruby/mruby) - mruby is the lightweight implementation of the Ruby language.
* [Opal](https://github.com/opal/opal#readme) - Opal is a Ruby to Javascript source-to-source compiler.
* [goby](https://github.com/goby-lang/goby) - Goby is an object-oriented interpreter language deeply inspired by Ruby as well as its core implementation by 100% pure Go.
* [GoRuby](https://github.com/goruby/goruby) - An implementation of Ruby written in Go.
* [grubby](https://github.com/grubby/grubby) - Grubby is an experimental ruby written in Golang.
* [Rubinius](https://github.com/rubinius/rubinius) - Rubinius is a modern language platform that supports a number of programming languages.
* [Topaz](https://github.com/topazproject/topaz) - A high performance ruby, written in RPython
* [Ruby-LLVM](https://github.com/ruby-llvm/ruby-llvm) - Ruby-LLVM is a Ruby language binding to the LLVM compiler infrastructure library.
* [erruby](https://github.com/johnlinvc/erruby) - ruby on erlang.

### <a name="yarv">2. YARV</a>
YARV(Yet another Ruby VM) is a bytecode interpreter writted in C that was developed for Ruby language.

Dla przykładu mamy poniższy kod.
``` Ruby
3.times { |n| puts n }
```

Po uruchomieniu dostajemy poniższy rezultat.
``` Ruby
0
1
2
```

Pytanie brzmi co się dziej pomiędzy wywołaniem kodu, a tym co dostajemy w odpowiedzi.

Zanim nasz kod zostanie uruchomiony musi przejść przez kilka procesów. W rzeczywistości nasz kod musi zostać przeczytam 3 razy zanim zostanie uruchomiony. Tak wygląda cały proces.

```
###############    ######################    ######################    #############    #######################
## Ruby Code ## => ## Tokenize(tokens) ## => ## Parse(AST nodes) ## => ## Compile ## => ## YARV Instructions ##
###############    ######################    ######################    #############    #######################
```

Tokenizing
Pierwszą rzeczy jaką robi interpreter jest tokenizowanie go. Oznacza to, że dzieli go na mniejsze kawałki, które mogą mieć jakiś sens. Dzięki modułowi Ripper dostępnemu w bibliotece standardowej możemy zobaczyć jak interpreter odczytuje nasz kod.

``` Ruby
require 'ripper'

code = "3.times { |n| puts n }"

Ripper.tokenize(code) # => ["3", ".", "times", " ", "{", " ", "|", "n", "|", " ", "puts", " ", "n", " ", "}"] 
```

W tym momencie Ruby jeszcze nie sprawdza czy to co wpisaliśmy ma jakikolwiek sens.


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
[tINTEGER(10)] [.] [tIDENTIFIER(times)]
```
Po tym jak ztokenizuje wszystko koćzy się Na tym kończy się pierwsze sprawdzenie kodu. Zaczęło się jakko tekst a teraz jest serią tokenów

Ripper
Jeśli chcemy sprawdzić jak działa tokenizowanie możemy użyć narzędzia ripper z biblioteki standardowej

``` Ruby
require 'ripper'

code = '3.times { |n| puts n }'

Ripper.tokenize(code) => => ["3", ".", "times", " ", "{", " ", "|", "n", "|", " ", "puts", " ", "n", " ", "}"] 
pp Ripper.lex(code) => 

[
 [[1, 0], :on_int, "3", EXPR_END],
 [[1, 1], :on_period, ".", EXPR_DOT],
 [[1, 2], :on_ident, "times", EXPR_ARG],
 [[1, 7], :on_sp, " ", EXPR_ARG],
 [[1, 8], :on_lbrace, "{", EXPR_BEG],
 [[1, 9], :on_sp, " ", EXPR_BEG],
 [[1, 10], :on_op, "|", EXPR_BEG|EXPR_LABEL],
 [[1, 11], :on_ident, "n", EXPR_ARG],
 [[1, 12], :on_op, "|", EXPR_BEG|EXPR_LABEL],
 [[1, 13], :on_sp, " ", EXPR_BEG|EXPR_LABEL],
 [[1, 14], :on_ident, "puts", EXPR_CMDARG],
 [[1, 18], :on_sp, " ", EXPR_CMDARG],
 [[1, 19], :on_ident, "n", EXPR_END|EXPR_LABEL],
 [[1, 20], :on_sp, " ", EXPR_END|EXPR_LABEL],
 [[1, 21], :on_rbrace, "}", EXPR_END]
]
```

Każda linia odnośi się do jednego tokena. Po lewej mamy numer lini, token jako symbol, następnie token a dalej text odnoszący się do tokena

Jak Ruby rozumie kod?
Ruby zamienia kod na serie tokenów ale jak jak rozumie kod i go uruchamia? Następną drogą jest parsowanie gdzie słowa są grupowane w sentencje i frazy które mają sens dla Rubiego. Uzywa do tego parser generator. Ruby używa do tego Bison dostajemy file z końcówką .y parse.y, która określa reguły gramatyczne a następnie 

W momencie tokenizowanie może być niepoprawny kod

Parsing
Jak już mamy podzielony kod zmienia to na text na coś co się nazywa AST(abstract syntax tree) i po tym may jeszcze jeden krok
Ripper.sexp

Compile

Czyli zmiana kodu na kod niższego rzędy

