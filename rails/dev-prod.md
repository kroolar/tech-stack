# Development vs Product

1. [Environments](#environments)
2. [Dev & Prod Differences](#devProd)

### <a name="environments">1. Environments</a>
The software environment can be defined as the machine on which the program is launched, as well as the software and a set of tools attached to this machine. Each Environment operates in different conditions and each has a different purpose and functions. The most common types of environments are:

- Development
- Test
- Staging
- Production

#### Development
The first environment the developer encounters it's **Development**. This environment runs on the developer's local computer. This environment is used for everyday work with software development. When writing code, most things don't work as they should, so the environment should in no way affect anything outside of it.

#### Test
Another environment is the **Test** environment. It allows you to perform previously written tests, thanks to which we can identify errors faster.

#### Staging
This environment should simulate the operation of a real system. Depending on the needs, access to it may be available to developers and testers who can test the final product in a friendly environment and also to whom we want to present the result of the work like final customer. Staging, as well as production, is launched on an external server to which only interested persons should have access.

#### Production
The production environment is the final environment in the software development process. The application goes there after thorough staging testing. The difference between production and staging is that it is usually publicly available and all changes are made live.

### <a name="devProd">2. Dev & Prod Differences</a>
The development environment should not affect anything but the local machine. Therefore, all activities that can to some extent influence external things should be limited or redirected in it. In Rails, we can set up different configurations for different environments in the **config/environments** path. The tools we use often provide their own implementation for different environments. Below are a few differences between the development and production environment.

#### DB
The development environment often uses a copy of the production environment database, although all sensitive data should be befuddle so that no one can access its true values. In production, we can additionally use a database replica, which is not necessarily needed in the development environment.

#### Storage
When using **ActiveStorage**, we have to set up some external provider, eg Google Cloud. In the case of the development environment, we do not want to modify anything on our cloud, therefore our "cloud" can be our local machine on which we will save new files.

#### Mailer
When testing e-mails in development, we do not want to send them to anyone, therefore, and at the same time we want to check that everything is working properly. For this purpose, the mailcache gem is most often used, which allows you to run a simple SMTP server on our local machine, thanks to which we will be able to intercept and display our messages in the browser.

#### Errors
When there are errors in the development environment, Rails displays a message with the errors. We do not want to show it to users in production, so most often we display a special view with a clear message and error number instead. In addition, we can attach an additional tool to collect bugs or send bugs directly via e-mail, thanks to which the development team will receive a notification.

#### Caching
Caching greatly relieves the production server and greatly increases the performance of the application, especially if it is used by many people. In production, we usually do not need caching, and sometimes it can even turn out to be an obstacle that misleads the developer. We can easily disable this configuration in config file.

``` Ruby
# config/environments/development.rb
config.action_controller.perform_caching = false
```

It is also possible to toggle the caching with a command.

```
rails dev:cache
```

#### Server
The server settings depend on the specific server that we use in our application, but here you will also find several settings that can be changed between environments. First of all, you have to take into account that the development environment will probably only be used by one user. In the development environment, we usually do not need an SSL connection, so we do not have to add any certificates to it.

#### Webpacker
During the release of our application in which we use a webpacker, it compiles all resources and creates one (or more) result files, which will later be available in the application. In a development environment, however, we don't want to do it that way because it would take too long. Therefore, when using the development environment, you should use **webpack-dev-server**, which supports HMR (hot module replacement), which significantly affects the loading of new changes.

```
./bin/webpack-dev-server
```

#### Variables
External applications with which our application is integrated should also have their development counterparts, especially if I send them requests that may change something on their side. For this purpose, we can use the **dotenv** library, which will allow us to manage credentials to our external applications, thanks to which it will not be possible to accidentally cause damage to an external application from the development environment.

#### Data migration
It happens that data migration affects not only our application but also an external application. In this case, we should either redirect the migration to the development environment of an external application or we can disable a specific piece of code by checking whether the migration is run on the production server.


``` Ruby
return unless Rails.env.production?
```

#### SSL
Thanks to SSL, we know that our connection with the server is trusted, therefore we should always have this configuration set on the production server. On the development server, however, usually there is no such need, so we can turn it off in the configuration without any problems.

``` Ruby
config.force_ssl = false
```

### Sources
- https://guides.rubyonrails.org/configuring.html
