
# Memento

Behavioral design pattern that is designed to manage the save and restore previously saved states.

### Problem

We want to build something like GIT repository. When applying the Memento pattern, we have to use 3 classes for this. The first one **Memento** is a just a snapshot that stores a given state. Sometimes it can also store information such as date, unique identifier or message. In our case, the Memento class will be **Commit**. Another class is **Originator**, which is responsible for saving and reading the state. In this case, it's **Project** class. The **Caretaker** is responsible for keeping all snapshots, adding new ones and reading existing ones. In our example, the role of **Caretaker** will be assumed by the **Repository** class.

``` Ruby
# Memento
class Commit
  attr_reader :state

  def initialize(state)
    @state = state
  end
end

# Originator
class Project
  attr_accessor :state

  def initialize
    @state = ''
  end

  def save
    Commit.new(@state)
  end

  def restore(memento)
    @state = memento.state
  end
end

# Caretaker
class Repository
  def initialize
    @commits = []
  end

  def history
    @commits
  end

  def add_commit(commit)
    @commits < commit
  end

  def commit(id)
    @commits[id]
  end
end

project = Project.new
repo = Repository.new

project.state = "Hello World!"
first_commit = project.save
repo.add_commit(first_commit)

project.state = "Hello Mars!"
second_commit = project.save
repo.add_commit(second_commit)

project.restore(repo.history[0])
project.state # => Hello World!
```

**Pros:**
- You can produce snapshots of the object’s state without violating its encapsulation
- You can simplify the originator’s code by letting the caretaker maintain the history of the originator’s state

**Cons:**
- The app might consume lots of RAM if clients create mementos too often
- Caretakers should track the originator’s lifecycle to be able to destroy obsolete mementos
- Dynamic programming languages can’t guarantee that the state within the memento stays untouched

**Sources:**
- https://refactoring.guru/design-patterns/memento
- https://refactoring.guru/design-patterns/memento/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-memento-1287f926fd0a
- https://github.com/KoKumagai/design-patterns-in-Ruby/blob/master/behavioral/memento/memento.rb
