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

**Concurrency** - Doing tasks at one time by quickly switching between them so that it may appear as if they are being performed simultaneously.

**Parallelism** - Doing multiple tasks at the same time.

Concurrency is most often used in programs such as web applications where we have many different threads, e.g. waiting for data to be fetched from DB or waiting for a server response. A virtual machine allows you to change the run of one thread while another is waiting.

We can create our own threads in Ruby using the **Thread** class from the standard library.

``` Ruby
Thread.new do
  loop{ puts 'First Thread'}
end

Thread.new do
  loop { puts 'Second Thread'}
end
```

After running this program, we will get nothing because all threads are terminating when the main thread ends. Therefore, when the main thread has terminated or is absent, the threads will not start.

We will delay the main thread for a second so our threads can start running.

``` Ruby
Thread.new do
  loop{ puts 'First Thread'}
end

Thread.new do
  loop { puts 'Second Thread'}
end

sleep 1
```

In response, we'll get a very long list of strings. Here, it only shows a small part of return.

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

What we can see is that the thread execution time is not even.

Threads in Ruby are normal objects so we can assign them to variables. 

``` Ruby
first_thread = Thread.new do
  loop{ puts 'First Thread'}
end

second_thread = Thread.new do
  loop { puts 'Second Thread'}
end
```

Instead of using the sleep method, we can join threads to the main thread with the join method.

``` Ruby
first_thread.join
second_thread.join
```

In this case, the program will run until we kill it.

For example, we will check how long it will take to connect to several pages in one thread. 

``` Ruby
require 'open-uri'

websites = [
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com"
]

start_time = Time.now

websites.each do |url|
  open(url)
end

puts (((Time.now - start_time) % 3600) % 60) # => 1.372596871
```

With the standard implementation, the time is over a second. Now let's try to run a separate thread for each connection.

``` Ruby
require 'open-uri'

threads = []

websites = [
  "https://google.com",
  "https://facebook.com",
  "https://github.com",
  "https://stackoverflow.com",
]

start_time = Time.now

websites.each do |url|
  t = Thread.new do
    open(url)
  end

  threads << t
end

threads.each { |t| t.join }

puts (((Time.now - start_time) % 3600) % 60) # => 0.461594078

```

In this case, the connection time to the same sites is less than half a second. 

However, it should be remembered that threads in Ruby map directly to threads of the opearating system, so creating too many threads at once does not necessarily speed up the whole process.

In summary, there can be many threads in Ruby, but only one can be active at a time. In the case of the wev development, this is not a problem because most of the code waits for responses from servers.

**Global Interpreter Lock(GIL)** - this is an algorithm used to prevent two threads from working simultaneously, interrupting the active thread from time to time so that the other thread can run. It allows for greater competition between threads of the same interpreter process, but results in a lack of performance enhancement for a program running on a multiprocessor computer. One of the reasons for such limitations is the C language in which Ruby is written that not work well in multiprocessing. 

**GIl** is not used in some Ruby implementations such as JRuby and Rubinus

Ruby also has a **Fiber** class which also uses concurrency in Ruby. The **Fiber** class allows for greater control in process management.

In the case of **Thread**, your operating system decides when to start and stop threads, but thanks to **Fibers**, we can decide about it ourselves. Additionally, they consume less memory than **Threads**, which translates into execution time. The last difference is that **Thread** run in the background and **Fiber** becomes the main thread until you stop them.

An example of the implementation of the Fiber class.

``` Ruby
f = Fiber.new do
  puts 'Process Start'
end
```

At this point, nothing has been started yet. We have to do this ourselves using the **resume** method.

``` Ruby
f.resume # => 'Process Start'
```

As we can see, the main thread does not have to be running for the above example to work properly.

We can stop the process by using the **yield** method. In this example, we will stop the thread after the first print to the text in the console.

``` Ruby
f = Fiber.new do
  puts 'Process Start'

  Fiber.yield

  puts 'Process End'
end

f.resume => 'Process Start' # => 'Process Start'
```
As you can see above, the process stop when it was supposed to stop. Now we can run it again.

``` Ruby
f.resume => 'Process End'
```

The thread started exactly where it stopped working the last time. We will try to start this thread again.

``` Ruby
f.resume => `resume': dead fiber called (FiberError)
```

In this example, Ruby throws an error because the thread has terminated.
