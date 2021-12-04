# Standard Modules

1. [Action Cable](#actionCable)
2. [Action Controller](#actionController)
3. [Action Dispatch](#actionDispatch)
4. [Action Mailbox](#actionMailbox)
5. [Action Mailer](#actionMailer)
6. [Action Pack](#actionPack)
7. [Action Text](#actionText)
8. [Action View](#actionView)
9. [Active Job](#activeJob)
10. [Active Model](#activeModel)
11. [Active Record](#activeRecord)
12. [Active Storage](#activeStorage)
13. [Active Support](#activeSupport)

- Abstract Controller?


### <a name="actionCable">1. Action Cable</a>
Pozwala na integracje z websocketami

### <a name="actionController">2. Action Controller</a>
Odpowiada z nadanie sensu żądanim http i zwróceniu odpowiedniej wiadoomośći. Najczęściej pobiera modyfikuje lub usuwa jakieś dane za pomocą modelu, a następnie tworzy html i zwraca go. Jest pośrednikiem międzt modelem a widokiem.

Jak wiele rzeczy w Railsach posiada pewną konwencje, która nakazuje tworznie nazw zawierających pluralize names. Dizęki temu bezszwowo może łączyć się z widokami oraz pozwala tworzyć jednolite ścieżki.

### <a name="actionDispatch">3. Action Dispatch</a>
Action Dispatch is responsible for few things reqarding web requests. The most important of them are:

- Parse information about the web request
- Handle routing
- Handling POST, PATHC and PUT parameters
- Handling HTTP caching logic
- Cookies and sessions

### <a name="actionMailbox">4. Action Mailbox</a>

**Responsible for:** Incoming mail management

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

### <a name="actionMailer">5. Action Mailer</a>
Moduł ten jest odpowiedzialny za wysyłanie maili. Mailery są bardzo podobne do kontrolerów. Posiadają własne widoki w app/views, zmienne instancji także są dostępne w widokach, także można używać layoutów i partiali, podobnie jak w kontrolerach możńa przekazywać parametry

Jak większośc w railsach psoiadają generatory

rails g mailer sample

### <a name="actionPack">6. Action Pack</a>
component responsible for providing Ruby language extensions, utilities, and other transversal stuff.


### <a name="actionText">7. Action Text</a>
Za ubogacenie wysiwyg editor

### <a name="actionView">8. Action View</a>
Action View is responsible for views in Rails and everything related to them.

All views are in _app/views_ folder. Folder names are related to the controllers, and the views inside are related to the controller's actions.

#### Templates
##### ERB
In this format it is possible to embed Ruby code directly into the view with <% %> and <%= %>

##### Builder
It is a more programmatic alternative to ERB. Most often it is used for generating XML content.

##### Jbuilder
It is a gem that comes with a Rails application by default. It is similar to the builder but the most used one for generating JSON.

#### Partials
They allow pieces of code to be broken down into smaller, reusable parts. When creating parts, we should precede them with an underscore, e.g. _'_nav.html.erb'_. We can pass additional parameters and even entire collections to it.

#### Layotus
Layouts provide a common interface for views with similar purposes.

#### Helpers
Rails provides many helpers available in views. The most important of them are:
- Formatting dates, strings and numbers
- Creating HTML links to images, videos, stylesheets, etc...
- Sanitizing content
- Creating forms
- Localizing content

### <a name="activeJob">9. Active Job</a>
This module is responsible for creating jobs, i.e. tasks that are performed asynchronously. In addition, it allows them to be queued and run according to the schedule provided. The Active Job module focuses on creating a coherent and logical infrastructure for the job runners no matter what we use.

Like many other things in rails, they have a generator to create them.

```
rails g job do_something
```

The files are located in the **app/jobs** folder and inherit from **ApplicationJob** by default.
They can be assigned to some queue and have only one **perform** method in which we can insert business logic.

``` Ruby
# app/jobs/do_something_job.rb

class DoSomethingJob < ApplicationJob
  queue_as :default

  def perform
    # Do something later
  end
end
```

We can run them using the **perform_later** method, which will do this task in the next free moment.

``` Ruby
DoSomethingJob.perform_later
```

Or at a specific time.

``` Ruby
DoSomethingJob.set(wait_until: Date.tomorrow.noon).perform_later
```

Like controllers, they have callbacks, but they are a bit different:
- before_enqueue
- around_enqueue
- after_enqueue
- before_perform
- around_perform
- after_perform

If we want to queue jobs on production, we have to use some additional library that will allow us to do so. By default, Rails stores jobs in RAM.

The most common example of a job in Rails is sending e-mail. The Action Mailer module is responsible for this.

``` Ruby
SampleMailer.hello(@user).deliver_later
```

### <a name="activeModel">10. Action Model</a>
Za modele

### <a name="activeRecord">11. Action Record</a>
Za baze danych

### <a name="activeStorage">12. Action Storage</a>
Za przechowywanie plikóœ

### <a name="activeSupport">13. Action Support</a>
component responsible for providing Ruby language extensions, utilities, and other transversal stuff.



