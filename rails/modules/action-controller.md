# Action Controller

Action Controller is an middleman between models and views in Rails.

### Naming Convention

By convention, the controller name should be plural. It doesn't force you, but following this convention, you don't need to set up any routes.

### Methods and Actions

The controller is a normal class that extends from **ApplicationController** and is located in **app/controllers**. After receive the request, Controller instance is created, and the method consistent with the request is executed, which is associated with the view of the same name.

``` Ruby
class UsersController < ApplicationController
  def index; end
end
```

### Parameters

Parameters in the web application can be sent in 2 ways. As part of the url and as part of the POST. Both are available in the controller using the params hash.

### Session

The application has sessions for each user, which is able to store a small amount of data between requests. You can use several methods:

- ActionDispatch::Session::CookieStore: Stores everything on the client.
- ActionDispatch::Session::CacheStore - Stores the data in the Rails cache.
- ActionDispatch::Session::ActiveRecordStore - Stores the data in a database using Active Record (requires the activerecord-session_store gem).

### Cookies

### Rendering

Controllers allow you to seamlessly render different formats within one action using the **respond_to** method.

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

Filters are responsible for carrying out some function in the controller life cycle:
- before_action
- after_action
- around_action

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

If you use helpers to create forms, Rails automatically generates and attaches a token to them, which allows you to prevent a forgery request.

``` html
<form accept-charset="UTF-8" action="/users/1" method="post">
<input type="hidden"
       value="67250ab105eb5ad10851c00a5621854a23af5489"
       name="authenticity_token"/>
</form>
```

### Request - Response

In each controller in rails you have the possibility to easily access information about both the request and the response. with the **request** and **response** methods.

### HTTP Authentications

Rails has three types of HTTP authentication methods built-in by default:

- Basic Authentication
- Digest Authentication
- Token Authentication

### Force HTTPS protocol
Only HTTP connection can be forced in the configuration settings. This is especially useful for production servers. This can be done with the following line.

``` Ruby
config.force_ssl = true
```

### Source
- https://guides.rubyonrails.org/action_controller_overview.html
- https://api.rubyonrails.org/v6.1.4/classes/ActionController/API.html

