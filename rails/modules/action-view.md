# Action View

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
