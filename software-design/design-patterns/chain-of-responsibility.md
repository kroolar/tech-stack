# Chain of Responsibility

A behavioral design pattern that allows a request to be passed along a chain of commands without having to associate the class sending the request with the class receiving it.

### Problem

In our ordering system, we have the option of paying by card, cash and even cryptocurrencies. We have several services that check whether they are able to handle a given payment. By creating a chain out of them, you are able to check, one by one, whether a given service is able to handle a given type of payment and in case of failure, you could pass parameters to the next service.

### Solution

``` Ruby
class PaymentHandler
  attr_accessor :successor
  
  def initialize(successor = nil)
    @successor = successor
  end
  
  def call(method)
    successor.present? && successor.call || error
  end
  
  private
  
  def success(message)
    puts message
  end

  def error
    raise 'Request could not be handled!'
  end
end

class CardPaymentHandler < PaymentHandler
  def call(method)
    can_handle?(method) &&
      success('The order has been paid for by Card') ||
      successor.call
  end

  private

  def can_handle?(method)
    method == 'Card'
  end
end

class CashPaymentHandler < PaymentHandler
  def call(method)
    can_handle?(method) &&
      success('The order has been paid for by Cash') ||
      successor.call
  end

  private

  def can_handle?(method)
    method == 'Cash'
  end
end

class CryptoPaymentHandler < PaymentHandler
  def call(method)
    can_handle?(method) &&
      success('The order has been paid for by Cryptocurrency') ||
      error
  end

  private

  def can_handle?(method)
    method == 'Cryptocurrency'
  end
end

payment = CardPaymentHandler.new(CashPaymentHandler.new(CryptoPaymentHandler.new))

payment.call(:cash) # => The order has been paid for by Cash
payment.call(:voucher) # => Request could not be handled!
```

**Pros:**
- You can control the order of request handling
- You can decouple classes that invoke operations from classes that perform operations (SRP)
- You can introduce new handlers into the app without breaking the existing client code (OCP)

**Cons:**
- Some requests may end up unhandled

**Sources:**
- https://refactoring.guru/design-patterns/chain-of-responsibility
- https://refactoring.guru/design-patterns/chain-of-responsibility/ruby/example
- https://medium.com/@dljerome/design-patterns-in-ruby-chain-of-responsibility-2868e40fe8c9
