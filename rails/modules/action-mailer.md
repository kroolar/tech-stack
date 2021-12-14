# Action Mailer
Action Mailer jest odpowiedzialny za wysyłanie maili z aplikacji. W rzeczywistośći jest adapterem dla Action Controller i Mail gem dlatego też działa w podobny sposób do kontrolerów.

Jak większość rzeczy w Rails posiada swój generator

rails g mailer notifier

który tworzy nowego maielra w app/mailers.

Klasa ta dziedziczy z ApplicationMAiler gdzie powinniśµy my ustawić pare rzeczy

MEtod w mailerze są powiązane z widokami tak jak jest to w przypadku kontrolerów.

Możemy wysłać maila na dwa sposoby, natychmiastowo albo przez deliver_later
