## Proxy

**Typ:** Strukturalny

**Cel:** Nadzoruje dostęp do obiektu oraz pozwala na definiowanie akcji przed lub po wystąpieniu zdarzenia.

### Problem
``` Ruby
class Account
  attr_reader :balance
  
  def initialize(balance = 0)
    @balance = balance
  end
  
  def deposit(amount)
    @balance += amount
  end
  
  def withdraw(amount)
    @balance -= amount
  end
end

class AccountProxy
  def initalize(account:, pin:)
    @account = account
  end
  
  def deposit(amount)
    check_access
    @balance += amount
  end
  
  def withdraw(amount)
    check_access
    @balance -= amount
  end
  
  def check_access
    raise_warning unless pin_valid?
  end
  
  def pin_valid?
    @pin == 1234
  end
  
  def raise_warning
    raise "#{@pin} is not a valid!"
  end
end
```

### ➕
- Można dodawać nowych pośredników bez modyfikacji istniejących serwisów
- Możemy łatwo zarządzać cyklem życia serwisu

### ➖
- Zwiększona złożoność kodu
- Zwiększony czas odpowiedzi

