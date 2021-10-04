# Virtual Machine

1. [Overview](#overview)
2. How Ruby Interprets code
  1. Code
  2. Tokenize
  3. AST
  4. Execute 
4. [Tokenizing](#tokenizing)
5. [Lexing](#lexing)
6. [Parsing](#parsing)
7. Garbage Collector

### <a name="tokenizing">2. Tokenizing</a>
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

### <a name="lexing">3. Lexing</a>
### <a name="parsing">4. Parsing</a>
Ruby zmienia tezt na coś co się nazywa abstract syntaxt tree (AST) Co to jest?

### <a name="parsing">5. Compiling</a>
Cpmpiling into bytecode

Ruby kompiluje AST na kod bitowy niższego rzędu, który nastęþnie jest uruchamiany przez maszyne wirtualną Rubiego

Możemy zajrzeć do wnętrze masyny wirtualnej za pomocą
``` Ruby
RubyVM::InstructionSequence.compile('').disassemble

Następnie maszyna wirtualna (YARV) step trough these instructions executes them
