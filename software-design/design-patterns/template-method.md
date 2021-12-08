# Template Method

Behavioral design pattern that allows you to define a common abstract scaffold of a base class that can then be overwritten by subclasses.

### Problem

We want to create a system that will allow us to save files in various formats. The scheme for creating different formats will be similar: _open the file_ then _add text_ and finally _save file_.

### Solution

``` Ruby
class File
  def initialize(name:, text:)
    @name = name
    @text = text
  end
  
  def create
    open(@name)
    add_body(@text)
    save
  end
  
  private
  
  def open
    raise 'Called abstract method: open'
  end
  
  def add_body
    raise 'Called abstract method: add_body'
  end
  
  def save
    raise 'Called abstract method: save'
  end
end

class DocFile < File
  def open(name)
    @doc = Doc.new(name)
  end
  
  def add_body(text)
    @doc.body = text
  end
  
  def save
    @doc.save
  end
end

class XlsFile < File
  def open(name)
    @xls = Xls.new(name)
    @worksheet = @xls.add_worksheet
  end
  
  def add_body(text)
    @worksheet.write(0, 0, text)
  end
  
  def save
    @xls.save
  end
end
```

**Pros:**
- You can let clients override only certain parts of a large algorithm, making them less affected by changes that happen to other parts of the algorithm
- You can pull the duplicate code into a superclass

**Cons:**
- Some clients may be limited by the provided skeleton of an algorithm
- You might violate the Liskov Substitution Principle by suppressing a default step implementation via a subclass
- Template methods tend to be harder to maintain the more steps they have

**Sources:**
- https://refactoring.guru/design-patterns/template-method
- https://refactoring.guru/design-patterns/template-method/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/template_method.md
- https://medium.com/@dljerome/design-patterns-in-ruby-template-method-753443f5a1c8
