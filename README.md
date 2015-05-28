# A Vagrant Box For Rails and Middleman Development

Based On Rails-Dev-Box

------------

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

-------------

### Getting Started
For OSX/Linux/Windows


1) Download and Install [Vagrant](http://www.vagrantup.com/downloads.html)

2) Download and Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

3) Download and open/install the appropriate [VM Virtualbox Extension Pack](https://www.virtualbox.org/wiki/Downloads)

-------------

### Git Clone the repo where ever you'd like the machine
```terminal
$ git clone https://github.com/dannyvassallo/rails-middleman-vagrant.git
$ cd rails-middleman-vagrant
```

------------
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
To suspend:
```terminal
vagrant suspend
```
To halt:
```terminal
vagrant halt
```
------------
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
------------
### Start Rails Server
don't use rails s. use this instead:

```
$ bin/rails s -b 0.0.0.0
```
------------
### Start A Middleman Server
don't use middleman s. use this instead:

```
bundle exec middleman s --port=3000
```
