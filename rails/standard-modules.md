# Standard Modules

1. [Action Cable](#actionCable)
2. [Action Controller](#actionController)
3. [Action Dispatch](#actionDispatch)
4. [Action Mailbox](#actionMailbox)
5. [Action Mailer](#actionMailer)
6. [Action Pack](#actionPack)
7. [Action Text](#actionText)
8. [Action View](#actionView)
9. [Action Job](#actionJob)
10. [Active Model](#activeModel)
11. [Active Record](#activeRecord)
12. [Active Storage](#activeStorage)
13. [Active Support](#activeSupport)

- Abstract Controller?


### <a name="actionCable">1. Action Cable</a>
Pozwala na integracje z websocketami

### <a name="actionController">2. Action Controller</a>
Odpowiada z nadanie sensu żądanim http i zwróceniu odpowiedniej wiadoomośći.

### <a name="actionDispatch">3. Action Dispatch</a>
Action Dispatch is really just bunch of code which has following responsibilities. It parses information about the web request, handles routing as defined by the user, and does advanced processing related to HTTP such as MIME-type negotiation, decoding parameters in POST, PATCH, or PUT bodies, handling HTTP caching logic, cookies and sessions

### <a name="actionMailbox">4. Action Mailbox</a>
Za zarządzanie skrzynką

### <a name="actionMailer">5. Action Mailer</a>
Za wysyłanie maili

### <a name="actionPack">6. Action Pack</a>
component responsible for providing Ruby language extensions, utilities, and other transversal stuff.


### <a name="actionText">7. Action Text</a>
Za ubogacenie wysiwyg editor

### <a name="actionView">8. Action View</a>
Za widoki

### <a name="actionJob">9. Action Job</a>
Pozwala na tworzenie jobów, kolejkowanie oraz uruchamianie ich. Active Job skupia się na tym aby stworzyć spójną i logiczną infrastrukture dla job runnerów bez względu na to jakiego typy ich użyjemy.

Jak wiele innych rzeczy w rails posiadają generator, który pozwala e tworzyć.

```
rails g job do_something
```

Pliki znajdują się w folderze app/jobs i powinny dziedziczyć z ApplicationJob
MOgą być przypisane do jakiejś kolejki i posiadają tylko jedną metode perform, w której wstawiamy logike
```
class GuestsCleanupJob < ApplicationJob
  queue_as :default

  def perform(*guests)
    # Do something later
  end
end
```

Możemy wykowywać je później ASAP
GuestsCleanupJob.perform_later guest

O jakiejś konkretnej porze
GuestsCleanupJob.set(wait_until: Date.tomorrow.noon).perform_later(guest)

6. Callbacks

### <a name="activeModel">10. Action Model</a>
Za modele

### <a name="activeRecord">11. Action Record</a>
Za baze danych

### <a name="activeStorage">12. Action Storage</a>
Za przechowywanie plikóœ

### <a name="activeSupport">13. Action Support</a>
component responsible for providing Ruby language extensions, utilities, and other transversal stuff.



