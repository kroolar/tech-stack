# Action Controller

Action Controller jest pośrednikiem pomiędzy modelami, a widokami.

### Naming Convention

Konwencja mówi o tym, że nazwa kontrolera powinna być liczbą mnogą. Nie wymusza ale podążając za tą konwencją nie trzeba ustawiać żadnych routesów.

### Methods and Actions

Kontroler jest zwykłą klasą, która dziedziczy z ApplicationController i jest umiejscowiona w app/controllers. Po otrzymaniu żądania tworzona jest instancja Kontrolera, i wykonywana jest metoda zgodna z żądaniem, któ©a jest powiązana z widokiem o takiej samej nazwie.

``` Ruby
class UsersController < ApplicationController
  def index; end
end
```

### Parameters

Parametry w aplikacji internetowej mogą zostać wysłane na 2 sposoby. Jako część adresu URL oraz jako część POST. Oba są dostępne w kontrolerze za pomocą hasha params.

### Session

Aplikacja ma sesje, dla każdgeo użytkownika, która jest w stanie przechowywać małą ilość danych pomiędzy żądaniami.Można skorzystac z kilku sposobów:

ActionDispatch::Session::CookieStore - Stores everything on the client.
ActionDispatch::Session::CacheStore - Stores the data in the Rails cache.
ActionDispatch::Session::ActiveRecordStore - Stores the data in a database using Active Record (requires the activerecord-session_store gem).

### Cookies

### Rendering

Kontrolery pozwalają na bezproblemowe renderowanie różnych formatów w obrębie jednej akcji za pomocą metody respond_to.

``` Ruby
class UsersController < ApplicationController
  def index
    @users = User.all
    respond_to do |format|
      format.html
      format.xml  { render xml: @users }
      format.json { render json: @users }
    end
  end
end
```

### Filters

Filtry są odpowiedzialne za wykonywanie jakiejs funckji w cyklu życia likacji. Railsy azapewniają 3 filtry before, after, around.

``` Ruby
class ApplicationController < ActionController::Base
  before_action :require_login
  
  private
  
  def require_login
    # Do something...
  end
end
```

### Request Forgery Protection

### Request - Response

### HTTP Authentications

### Streaming and File Downloads

### Log Filtering

### Rescue

### Force HTTPS protocol
