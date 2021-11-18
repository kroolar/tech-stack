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
Za zarządzanie skrzynką

### <a name="actionMailer">5. Action Mailer</a>
Moduł ten jest odpowiedzialny za wysyłanie maili. Mailery są bardzo podobne do kontrolerów. Posiadają własne widoki w app/views, zmienne instancji także są dostępne w widokach, także można używać layoutów i partiali, podobnie jak w kontrolerach możńa przekazywać parametry

Jak większośc w railsach psoiadają generatory

rails g mailer sample

### <a name="actionPack">6. Action Pack</a>
component responsible for providing Ruby language extensions, utilities, and other transversal stuff.


### <a name="actionText">7. Action Text</a>
Za ubogacenie wysiwyg editor

### <a name="actionView">8. Action View</a>
Action View jest odpowiedzialny za widoki w Rails i wszystko co jest z nimi powiązane w tym:
- Partiale
- Helpery
- Layouty

Widoki
Templates
Partials
Layouts
ERB

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



