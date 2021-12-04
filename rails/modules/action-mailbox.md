# Action Mailbox

Action Mailbox is responsible for incoming mail management.

#### What is it?

The **ActionMailbox** class converts incoming e-mails into **InboundEmail** objects using **Active Record**, stores original messages in the cloud using **ActiveStorage**, manages their lifecycle and handles routing.

#### Setup

If you want to start working with **ActionMailbox**, you need to run the following commands, which are responsible for creating the **InboundEmail** class in **ActiveRecord** and make sure **ActiveStorage** is set.

```
rails action_mailbox:install
rails db:migrate
```

#### Configuration

The configuration may vary depending on what service will be used. Below is a list of available services:

- Exim
- Mailgun
- Mandrill
- Postfix
- Postmark
- Qmail
- SendGrid

#### Example

This is an example of **ApplicationMailbox** class responsible for routing incoming e-mails.

``` Ruby
# app/mailboxes/application_mailbox.rb
class ApplicationMailbox < ActionMailbox::Base
  routing /^save@/i     => :forwards
  routing /@replies\./i => :replies
end
```

For the code to work properly, we also need to create **Forwards** and **Replies** classes, inheriting from **ApplicationMailbox**, which will be responsible for receiving messages. Fortunately, Rails provides a command to do this for us

```
rails generate mailbox forwards
```

#### IncinerationJob

This job is responsible for deleting old messages. By default, it is deleted after 30 days. You can change this setting in the configuration file by adding:

``` Ruby
# config/production.rb
config.action_mailbox.incinerate_after
```

#### Sources:
- https://guides.rubyonrails.org/action_mailbox_basics.html
