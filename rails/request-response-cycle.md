# Request-Response Cycle

A user opens his browser, types in a URL, and presses Enter. When a user presses Enter, the browser makes a request for that URL.
The request hits the Rails router (config/routes.rb).
The router maps the URL to the correct controller and action to handle the request.

The action receives the request, and asks the model to fetch data from the database.
The model returns a list of data to the controller action.
The controller action passes the data on to the view.
The view renders the page as HTML.
The controller sends the HTML back to the browser. The page loads and the user sees it.

- Żądanie do URL-a

- Rails sprawdza router (config/routes.rb)

``` Ruby
Rails.application.routes.draw do
  resources :users
end

 GET    /receipts(.:format)  receipts#index

```

Railsy szukają kontrolera o takiej nazwie, a następnie próbują dopasować akcje, żądania do metody w kontrolerze

``` Ruby
class UsersController < ApplicationController
  def index
    @users = Users.all
  end
end
```

W tym przypadku dodatkowo pobierają za pomocą modelu User dabe z bazy danych.

W tym momencie dane, użytkowników są udostępnione do widoku.
