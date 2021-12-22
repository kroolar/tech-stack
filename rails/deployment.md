# Deployment

Deployment in development is the process of deploying new changes to a production environment. It may differ depending on the tools used.

### First-time Configuration
#### Ruby & Rails
If we want to run our Rails application on the server, of course, we must have Ruby installed on it. Apart from that, we also have to make sure that we have the right version set, so it's best to get a version manager, e.g. rvm

```
rvm install ruby-3.0.0
rvm use 3.0.0
```

With Ruby Installed, we can finally install Rails.

```
gem install rails
```

#### Git
Of course we will have to fetch our latest code from some repository so we have to install git.

```
sudo apt-get install git
```

After downloading, it should be properly configured and connected to our repository, and then pull the project that we want to run on our server to the appropriate folder.

### Deployment
Having everything configured, we want to implement new changes to the production server.

#### Pull latest changes
The first thing we want to do is pull the latest changes from the repository.

```
git pull repo_name
```

#### Bundle Install
With the latest changes, we want to update our libraries.

```
bundle install
```

#### Migration
If we changed some structures in the database, we also need to start the migration so that the changes are available on the server.

```
rails db:migrate
```

#### Precompile Asssets
The next step is precompile assets. We can do it the easy way.

```
rails assets:precompile
```

#### Restart
The last step is to restart the server. Depending on what server you are using, this command may differ. Below is an example for a puma server.

```
systemctl restart puma
```

### Sources
