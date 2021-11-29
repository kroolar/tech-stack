# Request-Response Cycle

1. To start the request-response cycle, the user must enter an address in the browser click on a link. For examples it will be: _https://rails-app.com/users_

2. The request is sent to DNS servers, which are responsible for translating the domain name into an IP address. For example:  _https://rails-app.io/users_ _=> 212.85.96.183_

3. Having the IP address of our server, the browser is able to connect to it.

4. After receiving the request, the server processes the path given in the URL address and checks if any controller matches the given path. The Rails router is responsible for that process. In this case, the path **/users** corresponds to the controller **UsersController**.

``` Ruby
# config/routes.rb

Rails.application.routes.draw do
  resources :users, only: :index # GET /receipts(.:format) receipts#index
end
```

5. Each controller can have many methods, so in addition to the path itself, Rails must also check what action was sent to run the appropriate method. In this case, the router directs us to the **index**.

``` Ruby
# app/controllers/users_controller.rb

class UsersController < ApplicationController
  def index
    @users = Users.all
  end
end
```

6. In this case, the controller send query to the database using **User** model, retrive all users and assigned them to **@users** variable which is passed to the index view.

``` Ruby
User.all # => "SELECT `users`.* FROM `users` WHERE `users`.`deleted_at` IS NULL ORDER BY `users`.`name` ASC"
```

7. The data fetched in a given controller method is used using embedded Ruby in the view with the same name, if not specified otherwise.

``` Ruby
<% @users.map do |user| %>
  <%= user.name %>
<% end %>
```

8. By default controller return the HTML back to the browser with status **200**.
