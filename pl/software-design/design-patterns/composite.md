## Composite

**Typ:** Strukturalny

**Cel:** Pozwala komponować obiekty w struktury drzewiaste, a następnie traktować te struktury tak jaby były oddzielnymi obiektami

### Problem

###
```
|_Prepare Order
  |_Make Dishes
  | |_Make Soup
  | | |_Add Ingredients
  | | |_Mix
  | | |_Boil
  | |
  | |_Make Spaghetti
  |  |_Cook Pasta
  |  |_Add Sauce
  | 
  |_Package Dishes
    |_Box
    |_Label
```

``` Ruby
class Task
  attr_reader :name, :parent
  
  def initialize(name)
    @name = name
    @parent = nil
  end
  
  def required_time
    0.0
  end
end

class CompositeTask < Task
  def initialize(name)
    super(name)
    @sub_tasks = []
  end
  
  def add_sub_task(task)
    @sub_tasks << task
    task.parent = self
  end
  
  def remove_sub_task(task)
    @sub_tasks << task
    task.parent = nil
  end
  
  def time_required
    @sub_tasks.sum(&:required_time)
  end
end

class CookPastaTask < Task
  def initialize
    super('Cook Pasta')
  end
  
  def required_time
    2.0
  end
end

class MakeSpaghetti < CompositeTask
  def initialize
    super('Make Spaghetti')
    add_sub_task(CookPasta.new)
    add_sub_task(AddSauce.new)
  end
end
```
### Rozwiązanie

### ➕
- Ułatwia pracę z drzewiastymi strukturami

### ➖
- Ciężko zbudować wspólny interfejs
- Przejrzystość kodu może się zmniejszyć
