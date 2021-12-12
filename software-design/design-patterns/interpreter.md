# Interpreter

### Problem
### Solution

``` Ruby
class Parser
  def initialize(text)
    @tokens = text.split
  end
  
  def expression
    if token.nil? || tok
  end
  
  def next
    @to
  end
end

Parser.new("Add three to four").evaluate
```

**Pros:**
- Easy to implement
- Extendable and easy to change

**Cons:**
- Complex grammars are hard to maintain

**Sources:**
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/interpreter.md
- https://medium.com/@dljerome/design-patterns-in-ruby-interpreter-4b5375062897
