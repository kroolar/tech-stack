# Doctrine & Conventions

1. [Optimize for programmer happines](#one)
2. [Convention over Configuration](#two)
3. [The menu is omakase](#three)
4. [No one paradigm](#four)
5. [Exalt beautiful code](#five)
6. [Provide sharp knives](#six)
7. [Value integrated systems](#seven)
8. [Progress over stability](#eight)
9. [Push up a big tent](#nine)

### <a name="one">1. Optimize for programmer happines</a>

Rails is a framework that puts developers' happiness above everything else, even code performance. At first glance, this may seem absurd, but as life shows, the Rails community is still very popular. Rails tries to continue the concept of Ruby as a simple, readable, and easy-to-use language. One of Ruby's rules is **The Principle of Least Surprise**. Here's an example.

``` Ruby
[1, 2, 3].length # => 3
[1, 2, 3].size   # => 3
```

Thanks to this principle, the programmer gets exactly what he expects. Rails works similarly, but replaced this rule with **The Principle of The Bigger Smile** rule, which may be similar to **PoLS**, but thanks to it we can find in the code e.g. a method that takes forty-second object from an array.

``` Ruby
users = User.all
user.forty_two # => John Doe
```

The Inflector class is also a goof example of **PoBS**. This class converts string from singular to double.

``` Ruby
'People'.singularize => 'Person'
```

For programmers unfamiliar with Rails, this may seem funny, but this class is the foundation upon which the entire framework is based.

### <a name="two">2. Convention over Configuration</a>

Rails offers many conventions that a developer should follow. This allows you not to worry about trivial problems and focus on more important things. This also makes a little code that is much more readable. 

``` Ruby
has_many   :people
belongs_to :person
```

It also allows a lower entry level for beginners as they don't need to be aware of the things that are configured by default.

Of course, Rails is dynamic enough not to follow the convention, so it's important to know when such a change makes sense.

#### Naming Conventions
- Class names are **CamelCase**
- Methods and variables are **snake_case**
- Methods with a **?** suffix will return a boolean.
- Methods with a **!** suffix mean one of two things: either the method operates destructively in some fashion, or it will raise and exception instead of failing.

#### Database Naming Conventions
- Database tables use **snake_case**. Table names are **plural**.
- Column names in the database use **snake_case**, but are generally **singular**.

#### Model Naming Conventions
- Model class names use **CamelCase**. These are singular, and will map automatically to the plural database table name.
- Model attributes and methods use **snake_case** and match the column names in the database.
- Model files go in **app/models/#{singular_model_name}.rb**
- Relations use **snake_case** and follow the type of relation, so has_one and belongs_to are **singular** while has_many is **plural**
- Rails expects foreign keys in the database to have an **_id suffix**, and will map relations to those keys automatically if the names line up.

#### Controller Naming Conventions
- Controller class names use **CamelCase** and have Controller as a suffix. The Controller suffix is always singular. The name of the resource is usually **plural**
- Controller actions use **snake_case** and usually match the standard route names Rails defines (index, show, new, create, edit, update, delete)
- Controller files go in **app/controllers/#{resource_name}_controller.rb**

#### Routes Naming Conventions
- Route names are **snake_case**, and usually match the controller. Most of the time routes are plural and use the **plural** resources
- Singular routes are a special case. These use the **singular** resource and a **singular** resource name. However, they still map to a **plural** controller by default

#### Views Naming Conventions
- View file names, by default, match the controller and action that they are tied to
- Views go in** app/views/#{resource_name}/#{action_name}.html.erb**

### <a name="three">3. The menu is omakase</a>

Omakase is a phrase used when ordering food in restaurants and means "I'll leave it to you".

Rails takes the burden of the programmer's individual choices in favor of the programmer's choices. It's important especially at the beginning of journey. Programmer may not realize which tool is best for this, so Rails does it for us. There are several reasons for this:
  1. If a large number of programmers use the same tool and they share experiences, it is easier to solve bugs and create better tools.
  2. Rails has many moving parts that are connected and affect each other. Having the same set of tools, we are sure that the interactions between them will be the same.
  3. As in the case of conventions, we can still replace existing tools with other ones

### <a name="four">4. No one paradigm</a>

Rails doesn't have a one main pradigm. It can be said that he has many of them and to some extent tries to combine and mix them. This makes it very dynamic and therefore we can tailor it to our needs.

### <a name="five">5. Exalt beautiful code</a>

We write code so that it is understandable not only for the computer but also for programmers. This is because most of the time we read the code, so it is important that the code is as understandable as possible to the person who sees it for the first time(or to ourselves after a long period of time).

It is impossible to precisely define what a readable code looks like, but when we see it, we immediately know that it is.

Rails focuses on more subtle differences in addition to the readable syntax.

``` Ruby
if people.include? person

if person.in? people
```

These two staements do exactly the same, but reading them we have completely different ideas about the code written.

### <a name="six">6. Provide sharp knives</a>

Thanks to monkey pathcing, Rails allows you to override built-in classes. Does that mean you should be doing this? It depends. At the beginning, we will definitely not want to use these functionalities(we will not even know how), but with time, when we will be more experienced and we will know how to use these functionalities and we will know what the consequences are, it can be very useful for us, which is why Rails trusts enough to us that I will save these tools, hoping that we will not hurt ourselves.

### <a name="seven">7. Value integrated systems</a>

Rails like monoliths. They deal with frontend, backend and database management. Thanks to the use of a monolith, the application can share its resources both on the client side and on the server side. It is much easier and faster to create such applications (which is why Rails is a frequent choice among startups). The application in such an architect is also more resistant to errors. Of course, the monolith also has a few drawbacks that show up especially in the later stages of the project. In recent years, microservices have become very popular and Rails meets the needs of users by providing a generator that allows the user to create only server applications.

```
rails g new app_name --api
```

Even so, Rails's main goal is still to be one fully integrated system. But if you want to go another way, go ahead.

### <a name="eight">8. Progress over stability</a>

New functionalities should encourage changes in old projects. In the long run, progress is much more valuable, even at the expense of the current situation. Upgrading to the next version is often expensive, especially for large applications, but it is certainly worth it. Therefore, if we want to get new functionalities, we must take into account the fact that we have to use the latest versions, even though it will cost us the time spent on adapting them to new standards.

The same principle applies to the entire Rails community. Even a place in groups such as Rails Core or Rails Commiters does not last forever, and you have to work actively to get there and stay there.

### <a name="nine">9. Push up a big tent</a>

Rails was built around controversial ideas. This community may have closed itself off to new ideas, but is instead open to discussion even when some ideas do not fit at all with the initial concepts.

The best example of this is an application that only creates an API. This idea completely misses the initial assumptions and even the creator of Rails was against it but the community demanded it and now we can easily separate the client application from the server part.

Sources:
- https://rubyonrails.org/doctrine/
- https://gist.github.com/iangreenleaf/b206d09c587e8fc6399e

