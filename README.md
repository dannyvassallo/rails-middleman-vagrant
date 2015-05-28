# A Vagrant Box For Rails and Middleman Development
##Based On Rails-Dev-Box

### What's in it?

* Development tools
* Git
* Ruby 2.2
* Bundler
* SQLite3, MySQL, and Postgres
* Databases and users needed to run the Active Record test suite
* System dependencies for nokogiri, sqlite3, mysql, mysql2, and pg
* Memcached
* Redis
* RabbitMQ
* An ExecJS runtime
* Foreman
* Middleman

### Git Clone the repo where ever you'd like the machine
```terminal
$ git clone 'this-repo'
$ cd 'this-repo'
```

### Vagrant Box

To Start up your VM:
```terminal
$ vagrant up
```
To SSH in to the VM:
```terminal
$ vagrant ssh
```
Navigate to synced folders:
```terminal
$ cd /vagrant
```

### PostGres Credentials
Taken from [here](https://gist.github.com/eliotsykes/3e74172c43c2e8787dd9)

update your config/database.yml with these DB credentials:

```ruby
development:
  …
  username: coderelf
  password: password


test:
  …
  username: coderelf
  password: password
```

To enable Hstore:

change 'MY_DATABASE' to your database name.

```terminal
$ sudo su postgres -c "psql MY_DATABASE -c 'CREATE EXTENSION hstore;'"
```

### Start Rails Server
don't use rails s. use this instead:

```
$ bin/rails s -b 0.0.0.0
```

### Start A Middleman Server
don't use middleman s. use this instead:

```
bundle exec middleman s --port=3000
```
