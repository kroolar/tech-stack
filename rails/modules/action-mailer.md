# Action Mailer

**Action Mailer** is responsible for sending e-mails from the application. In fact, it is an adapter for **Action Controller** and **Mail** gem and therefore it works in a similar way to controllers.


### Overview

Like most things in Rails, the mailers module has its own generator.

```
rails g mailer notifier
```

Which creates a new mailer in app/mailers folder.

``` Ruby
class NotifierMailer < ApplicationMailer
end
```

Before we start working with mailers, we should set the default layout and message sender in the **ApplicationMailer** file.

``` Ruby
class ApplicationMailer < ActionMailer::Base
  default from: "from@example.com"
  layout 'mailer'
end
```

Methods in the mailer are assign to views just like controllers. The following method is assign to the view found in app/views/notifier_mailer/payment.html.erb. Also we can pass parameters as well as in the case of controllers.

``` Ruby
class NotifierMailer < ApplicationMailer
  def payment
    @price = params[:price]
    @user = params[:user]
    mail(to: @user.email, subject: 'New Payment')
  end
end
```

As in the case of normal views in mail idks, we can use the variables that we defined in the related method.

It is common practice to create a view in parallel with the **.text.erb** extension because not all mailboxes can support HTML views.

If we want to handle the above e-mail, we can do it in two ways. The first is to send it right away using the **deliver_now** method.

``` Ruby
NotifierMailer.payment(user: current_user, price: 99).deliver_now
```

The second way is to send it asynchronously using the **deliver_later** method. In this case, we must remember that **Active Job** should be configured.

```
NotifierMailer.payment(user: current_user, price: 99).deliver_later
```

We can also attach additional files to the e-mails using the attachments method. In this case, we must remember whether **Active Storage** is configured in our application.

``` Ruby
def payment
  attachments.inline['invoice.pdf'] = File.read('/path/to/invoice.pdf')
end
```

### Callbacks

Action Mailer, like controllers, has three callbacks:

- before action
- after action
- around action

### Configuration

Before starting to work with e-mails, we should first prepare the configuration of this module for various environments. Below is an example configuration.

``` Ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address:              'smtp.gmail.com',
  port:                 587,
  domain:               'example.com',
  user_name:            '<username>',
  password:             '<password>',
  authentication:       'plain',
  enable_starttls_auto: true,
  open_timeout:         5,
  read_timeout:         5 }
```

### Sources
- https://guides.rubyonrails.org/action_mailer_basics.html
- https://api.rubyonrails.org/v6.1.4/classes/ActionMailer/Base.html
