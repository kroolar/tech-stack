# Composite

Structural design pattern that allows works with tree structures objects.

### Problem

We have a lot of teams in our company. Some departments are further broken down into even smaller divisions. This is an example of a company structure.

```
|__ Company
    |__ Development
    |   |__ Design
    |   |   |__ UX/UI
    |   |   |__ Graphic
    |   |
    |   |__ FrontEnd
    |   |__ Backend
    |
    |__ Executive
        |__ Box
        |__ Label
```

To use the **Composite** pattern, we need to distinguish three types of classes:
- **Component**: Base class that defines a common interface for all components. In this case it will be **Team**
- **Composite**: A higher order component that is built from smaller components, e.g. a **Design** team
- **Leaf**: Low-order component that does not break into smaller parts, e.g. **Graphic** team

In our case, the component will be the **Team** class, which contains the name, the unassigned parent and the number of employees set to 0 by default.

``` Ruby
class Team
  attr_accessor :name, :parent

  def initialize(name)
    @name = name
    @parent = nil
  end

  def employees
    0
  end
end
```

Now we want to build the lowest order class based on the **Team** class.

``` Ruby
class GraphicTeam < Team
  def initialize
    super('Graphic')
  end

  def employees
    4
  end
end
```

To build a team composed of other teams, we need to build a composite class, which will be responsible for managing the components.

``` Ruby
class CompositeTeam < Team
  def initialize(name)
    super(name)
    @sub_teams = []
  end

  def add_sub_team(team)
    @sub_teams << team
    team.parent = self
  end

  def remove_sub_team(team)
    @sub_team.delete(team)
    team.parent = nil
  end

  def employees
    @sub_teams.sum(&:employees)
  end
end
```

Having a composite class, we are already able to build more complex structures.

``` Ruby
class DesignTeam < CompositeTeam
  def initialize
    super('Design')
    add_sub_team(Graphic.new)
    add_sub_team(UXUI.new)
  end
end

class DevelopmentTeam < CompositeTeam
  def initialize
    super('Development')
    add_sub_team(Design.new)
    add_sub_team(Frontend.new)
    add_sub_team(Backend.new)
  end
end
```

**Pros:**
- You can work with complex tree structures more conveniently: use polymorphism and recursion to your advantage
- You can introduce new element types into the app without breaking the existing code, which now works with the object tree (OCP)

**Cons:**
- It might be difficult to provide a common interface for classes whose functionality differs too much. In certain scenarios, you’d need to overgeneralize the component interface, making it harder to comprehend

**Sources:**
- https://refactoring.guru/design-patterns/composite
- https://refactoring.guru/design-patterns/composite/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/composite.md
- https://medium.com/@dljerome/design-patterns-in-ruby-composite-e815a25467b5
