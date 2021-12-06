# Bridge

It separates the abstractions of its implementation, so you can modify these two elements independently.

### Problem

Mamy klasę Users, która pozwala pobierać dane z różnych zasobów. Dodając nowe metody, będziemy musieli w nihc uwzględnić wszystkie zewnętrzne zasoby, z których będziemy pobierać dane. Jednocześnie dodająć kolejną integracje będziemy musieli wszystko modyfikować.

``` Ruby
class Users
  def all(from)
    if from == 'CRM'
      # Get Users from CRM
    else
      # Get Users from application DB
    end
  end
end
```

### Solution

Wzorzec Bridge pozwala na oddzielenie abstrakcji od implementacji co pozwoli na osobne rozwijanie obu tych części oddzielnie

``` Ruby
  class User
    def initialize(implementation)
      @implementation = implementation
    end
    
    def all
      @implementation.all
    end
  end

  class AppUsers
    def all
      # Get application Users
    end
  end
  
  class CRMUsers
    def all
      # Get users from CRM
    end
  end
```

**Pros:**
- You can create platform-independent classes and apps
- The client code works with high-level abstractions. It isn’t exposed to the platform details
- You can introduce new abstractions and implementations independently from each other (OCP)
- You can focus on high-level logic in the abstraction and on platform details in the implementation (SRP)

**Cons:**
- You might make the code more complicated by applying the pattern to a highly cohesive class

**Sources:**
- https://refactoring.guru/design-patterns/bridge
- https://refactoring.guru/design-patterns/bridge/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-bridge-7aebb1b7bbc6
