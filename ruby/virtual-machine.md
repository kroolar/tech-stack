# Virtual Machine
Ruby implementaions MRI YARV jruby
1. [Ruby Language](#rubyLanguage)
2. [YARV](#yarv)
3. [Garbage Collector](#gc)
4. [Concurenncy & Pallarelis](#cp)

ZALETY I WADY METAPROGRAMOWANIA

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
**YARV**(Yet another Ruby VM) is a bytecode interpreter writted in **C** that was developed for Ruby language.

We will use the following code in all examples.

``` Ruby
x = 2 + 3
```

After running this code, we will get the following result.

```
ruby code.rb
=> 5
```

The question is what happens between calling the code and what we get in response.

Before our code is run, it has to go through several processes. In fact, our code needs to be read 3 times before it is run. This is the whole process.

```
###############    ######################    ######################    #############    #######################
## Ruby Code ## => ## Tokenize(tokens) ## => ## Parse(AST nodes) ## => ## Compile ## => ## YARV Instructions ##
###############    ######################    ######################    #############    #######################
```

#### Tokenizing
The first thing the interpreter does is tokenize it. Ruby reads all the code first, and then tokenizes it. Tokenization means that it converts the code into a series of tokens, i.e. words that may make sense.

Thanks to the Ripper module available in the standard library, we can see how the interpreter reads our code.

``` Ruby
Ripper.tokenize(code) # => ["x", " ", "=", " ", "2", " ", "+", " ", "3"]
```

After tokenizing everything, that's the end of the first code check. It started out as a text and is now a series of tokens. We can read more information about tokens with **lex** method.

``` Ruby
[
 [[1, 0], :on_ident, "x", EXPR_CMDARG],
 [[1, 1], :on_sp, " ", EXPR_CMDARG],
 [[1, 2], :on_op, "=", EXPR_BEG],
 [[1, 3], :on_sp, " ", EXPR_BEG],
 [[1, 4], :on_int, "2", EXPR_END],
 [[1, 5], :on_sp, " ", EXPR_END],
 [[1, 6], :on_op, "+", EXPR_BEG],
 [[1, 7], :on_sp, " ", EXPR_BEG],
 [[1, 8], :on_int, "3", EXPR_END]
]
```

As we can see here, we have lines, a symbol specifying the type of the token, its textual representation, and where it ends and begins.

At this point, Ruby doesn't yet check to see if what we typed makes any sense.

#### Parsing
Now that we have the tokenized code, it's time to parse. When Ruby parses, it changes the text to something called an Abstract Syntax Tree (AST) which is a representation of your code.

``` Ruby
pp Ripper.sexp(code) # =>

[:program,
 [[:assign,
   [:var_field, [:@ident, "x", [1, 0]]],
   [:binary, [:@int, "2", [1, 4]], :+, [:@int, "3", [1, 8]]]]]]
```

Ruby uses a tool called **Bison** for parsing. After parsing, we get a file with the extension **.Y**, which will later be converted into a file understandable for the **C** language.

At this point, Ruby already knows how to run your program.

#### Compiling
In the next step, Ruby compiles the **AST** to a low-order bytecode. We can see what it looks like using the **RubyVM :: InstructionSequence** module.

``` Ruby
puts RubyVM::InstructionSequence.compile(code).disassemble

== disasm: #<ISeq:<compiled>@<compiled>:1 (1,0)-(1,9)> (catch: FALSE)
local table (size: 1, argc: 0 [opts: 0, rest: -1, post: 0, block: -1, kw: -1@-1, kwrest: -1])
[ 1] x@0
0000 putobject                    2                                   (   1)[Li]
0002 putobject                    3
0004 opt_plus                     <callinfo!mid:+, argc:1, ARGS_SIMPLE>, <callcache>
0007 dup
0008 setlocal_WC_0                x@0
0010 leave
```
The code compiled in this way will then be executed step by step by the Ruby Virtual Machine.

### <a name="gc">3. Garbage Collector</a>
**Garbage Collector** is a process used in high-level languages to manage memory. The classic version of Ruby (MRI) uses a **GC** called **mark-and-sweep** which was invented in 1960. 

Garbage Collector solves 3 problems:
- allocate memory for use by new objects
- identify which objects your program is no longer using
- reclaim memory from unused objects

#### Mark and Sweep Algorithm
Ruby uses tricolor mark. Divides the objects into 3 categories of white, gray and black flag.

First, Ruby checks all objects and white flags those that should not be removed, and gray flags those that might have some references to the objects in use. The next phase checks gray flag and their connections to other objects. If it should not be removed, the black flag will be mark, and if the object has no active references, it turns the flag white. This is how the first phase ends.

The next and final phase is the sweep phase, which removes all objects that have been marked with a white flag.

### <a name="cp">4. Concurrency & Parallellism</a>
Concurrency - Robienie zadań w jednym czasie poprzez szybką zmiane pomiędzy nimi tak, że może się wydawać, że są wykonywane jednocześnie.

Parallelism - Robienie wielu zadań w tym samym czasie równocześnie

Concurrency jest najczęściej wykorzystywane w programach takich jak aplikacje webowe gdzie mamy wiele różnych wątków np. oczekwiane na pobranie danych lub czekanie na utworenie połączenia. Wirtualna maszyna pozwala na zmiane uruchomienie jednego wątku wtedy kiedy inny czeka

Concurrency jest wykorzystywane dzięki Threads. Każdy program może mieć wiele wątków oraz musi mieć co najmniej jeden wątek, który jest wątkiem głównym.

Możemy utworzyć nowy wątek za pomocą klasy Thread z biblioteki standardowej

``` Ruby
Thread.new do
  loop{ puts 'First Thread'}
end

Thread.new do
  loop { puts 'Second Thread'}
end
```

Po uruchomieniu tego programu nie dostaniemy nic ponieważ wszystkie wątki kończą swoje działanie w momencie zakończenia głównego wątku. Dlatego opóźnimy go o sekunde

``` Ruby
Thread.new do
  loop{ puts 'First Thread'}
end

Thread.new do
  loop { puts 'Second Thread'}
end

sleep 1
```

W odpowiedzi dostaniemy bardzo długą liste stringów. Tutaj jest tylko jej mały wycinek

```
Second Thread
Second Thread
Second Thread
Second Thread
Second Thread
Second Thread
Second Thread
First Thread
First Thread
Second Thread
Second Thread
Second Thr
```

To co możemy zauwazyć to to, że czas przyporządkownia jednego watku nie jest równomierny. Po drugie jak możemy zauważyć na końcu Ostani wątek nie zdołał się wykonać do końca

Wątki w Rubym są normalnymi obiektami klasy Thread dlatego możemy je przypisać do zmiennych

``` Ruby
first_thread = Thread.new do
  loop{ puts 'First Thread'}
end

second_thread = Thread.new do
  loop { puts 'Second Thread'}
end
```

Zamiast używać metody sleep możemy dołączyć wątki do głównego wątku za pomocą metody join.

``` Ruby
first_thread.join
second_thread.join
```

W tym przypadku program będzie działał dopóki go nie zabijemy.

Dla przykładu sprawdzimy ile czasu zajmie połączenie z kilkoma stronami w jednym wątku.

``` Ruby
require 'open-uri'

websites = [
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com",
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com"
]

start_time = Time.now

websites.each do |url|
  open(url)
end

puts (((Time.now - start_time) % 3600) % 60)
```

4.434610808


``` Ruby
require 'open-uri'

threads = []

websites = [
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com",
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com"
]

start_time = Time.now

websites.each do |url|
  t = Thread.new do
    open(url)
  end

  threads << t
end

threads.each { |t| t.join }

puts (((Time.now - start_time) % 3600) % 60)
```

1.030195963

Wątki w Ruby mapują sie wątki systemu operacyjnego

Może istnieć wiele wątków, ale tylko jeden jest aktywny. W przypadku internetu nie jest to problem ponieważ kod w większości czeka na odpowiedzi z serwerów

Wątki w Rubym nadają sie do prostych rzeczy ale nie powinno się ich stosować w przypadku jakiś kalkulacji
Global Interpreter Lock zapobiega dwóm wątkom pracować jednocześnie więc jeden wątke będzie co jakiś czas przerywany, żeby drugi mógł pracować. Ma to na celu zapobieganie temu, że jeden wątek jest cały czas odpalony,
Pozwala na większą konkurencyjność między wątkami tego samego procesu interpretera ale powoduje brak zwiększenia wydajności programu uruchomionego na komputerze wieloprocesorowym. Jednym z powodów takich ograniczeni jest język C w któ©ym jest naisany Ruby, a nie działa on dobrze w trybie wieloprocesorowym

GIl nie jest stosowany w niektórych implementacjach Rubiego takich jak JRuby oraz Rubinus
