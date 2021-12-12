# Interpreter

A behavioral design pattern that defines the grammar along with its translation, which is then interpreted into a programming language. This pattern is often used to build domain specific languages.

### Problem

We want to build a calculator into which we will be able to enter text data, and then calculate the result based on it.

The program will be divided into two parts:
- parsing the program text into an abstract syntax tree (AST)
- interpreting the AST

It is worth paying attention to the similarities to the composite pattern, which also works with tree structures.

### Solution

At the beginning, we will define 2 objects that will be responsible for the numbers. These clusters represent so-called **terminal**(leaf) that are low-order components that do not use other components.

``` Ruby
class Two
  def evaluate
    2
  end
end

class Three
  def evaluate
    3
  end
end
```

Then we can create so-called **non-terminals**, i.e. higher-order components that will use other components. In this case, it will be the **Add** and **Subsract** classes.

``` Ruby
class Add
  def initialize(expression1, expression2)
    @expression1 = expression1
    @expression2 = expression2
  end

  def evaluate
    @expression1.evaluate + @expression2.evaluate
  end
end

class Substract
  def initialize(expression1, expression2)
    @expression1 = expression1
    @expression2 = expression2
  end

  def evaluate
    @expression1.evaluate - @expression2.evaluate
  end
end
```
 
The parser is responsible for breaking up the text into smaller parts called **tokens** and then creating the **AST**.
 
``` Ruby
class Parser
  def initialize(text)
    @tokens = text.split
  end

  def next_token
    @tokens.shift
  end

  def expression
    token = next_token

    if token == 'add'
      Add.new(expression, expression)
    elsif token == 'substract'
      Substract.new(expression, expression)
    elsif token == 'three'
      Three.new
    elsif token == 'two'
      Two.new
    else
      expression
    end
  end
end

parser = Parser.new 'add three to to'
ast = parser.expression
ast.evaluate # => 5
```

We can now wrap it with the **Calculator** class, which will allow us to calculate it in a simple way.

``` Ruby
class Calculator
  def calculate(text)
    parser = Parser.new(text)
    ast = parser.expression
    ast.evaluate
  end
end

calculator = Calculator.new
calculator.calculate('add three to two') # => 5
calculator.calculate('add three to three') # => 6
```

**Pros:**
- Easy to implement
- Extendable and easy to change

**Cons:**
- Complex grammars are hard to maintain

**Sources:**
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/interpreter.md
- https://medium.com/@dljerome/design-patterns-in-ruby-interpreter-4b5375062897
