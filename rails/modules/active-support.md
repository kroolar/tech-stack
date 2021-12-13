# Active Support

Active Support is responsible for providing extensions to Ruby. In Ruby On Rails it is loaded by default, so often beginner programmers may have problems not finding their favorite methods in pure Ruby.

If we want to disable automatic loading of Active Support, we just need to change the property from true to false.

``` Ruby
# config/application.rb
config.active_support.bare = false
```

Some examples of using the Active Support module.

``` Ruby
# Return current time
Time.current # => => Mon, 13 Dec 2021 12:59:34 GMT +00:00

# Check if element exist in array
2.in? [2, 20, 30] # => true

# Return element if exist or nil if it's empty
"String".presence # => "Presence"
```

### Sources
- https://guides.rubyonrails.org/active_support_core_extensions.html
