# Action Mailer

Action Mailer jest odpowiedzialny za wysyłanie maili z aplikacji. W rzeczywistośći jest adapterem dla Action Controller i Mail gem dlatego też działa w podobny sposób do kontrolerów.

Jak większość rzeczy w Rails posiada swój generator

```
rails g mailer notifier
```

który tworzy nowego maielra w app/mailers.

``` Ruby
class ApplicationMailer < ActionMailer::Base
  default from: "from@example.com"
  layout 'mailer'
end

class UserMailer < ApplicationMailer
end
```

Klasa ta dziedziczy z ApplicationMAiler gdzie powinniśµy my ustawić pare rzeczy

MEtod w mailerze są powiązane z widokami tak jak jest to w przypadku kontrolerów.

Możemy wysłać maila na dwa sposoby, natychmiastowo albo przez deliver_later

class UserMailer < ApplicationMailer
  default from: 'notifications@example.com'

  def welcome_email
    @user = params[:user]
    @url  = 'http://example.com/login'
    mail(to: @user.email, subject: 'Welcome to My Awesome Site')
  end
end
