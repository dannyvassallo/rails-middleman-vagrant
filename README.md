# A Vagrant Box For Rails and Middleman Development

Based On Rails-Dev-Box

------------

## What's in it?

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

## Getting Started
For OSX/Linux/Windows


1) Download and Install [Vagrant](http://www.vagrantup.com/downloads.html)

2) Download and Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

3) Download and open/install the appropriate [VM Virtualbox Extension Pack](https://www.virtualbox.org/wiki/Downloads)

4) Ensure git CLI on host machine

/// FOR WINDOWS ONLY SKIP AHEAD TO VAGRANT BOX SECTION IF USING OSX ///

5) Download and Install [PuTTy](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) [putty.exe](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe)

6) Download and Install [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) [puttygen.exe](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)

-------------

#### Git Clone the repo where ever you'd like the machine
```terminal
$ git clone https://github.com/dannyvassallo/rails-middleman-vagrant.git
$ cd rails-middleman-vagrant
```

------------
## Vagrant Box

###Macintosh OS X

####Setting Memory and Processor Power in Vagrant

navigate to the cloned repo
```
cd rails-middleman-vagrant
```

Open 'Vagrantfile' with sublime text

Replace it's contents with these changing the number following ```v.cpus```
to update the number of processor cores and changing the number following
```v.memory``` to your desired RAM specs.

```
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.vm.hostname = 'danny-rails-middleman'

  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision :shell, path: 'bootstrap.sh', keep_color: true

  config.vm.provider 'virtualbox' do |v|
    v.cpus = 2
    v.memory = 2048
  end

end
```

If you've run ```vagrant up``` before setting up your memory run:

```
$ vagrant destroy
$ vagrant up && vagrant provision
```


######Check Your Memory has been successfully changed
```
$ cd rails-middleman-vagrant
$ vagrant up
$ vagrant ssh
$ free -m
```
The total memory reported should match closely to the ```v.memory``` inputted.


#### Start Vagrant

To Start up your VM
```terminal
$ vagrant up
```
To SSH in to the VM:
```terminal
$ vagrant ssh
```
Navigate to synced folders directory:
```terminal
$ cd /vagrant
```

#### Stop Vagrant

To suspend:
```terminal
vagrant suspend
```
To halt:
```terminal
vagrant halt
```

###Windows XP/7/8

####Setting Memory and Processor Power in Vagrant

navigate to the cloned repo
```
cd rails-middleman-vagrant
```

Open 'Vagrantfile' with sublime text

Replace it's contents with these changing the number following ```v.cpus```
to update the number of processor cores and changing the number following
```v.memory``` to your desired RAM specs.

```
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.vm.hostname = 'danny-rails-middleman'

  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision :shell, path: 'bootstrap.sh', keep_color: true

  config.vm.provider 'virtualbox' do |v|
    v.cpus = 2
    v.memory = 2048
  end

end
```

If you've run ```vagrant up``` before setting up your memory run:

```
$ vagrant destroy
$ vagrant up && vagrant provision
```


######Check Your Memory has been successfully changed
```
$ cd rails-middleman-vagrant
$ vagrant up
$ vagrant ssh
$ free -m
```
The total memory reported should match closely to the ```v.memory``` inputted.


#### Start Vagrant

To Start up your VM in cmd or powershell
```terminal
$ vagrant up
```
#### 1) Generate SSH Keys With PuTTyGen (You only do this once)

* Open puttygen.exe

* Click the "Load" button

* To the right of Filename at the bottom change the drop down from
"PuTTy Private Key Files (*.ppk)" to "All Files (*)"

* Navigate to the cloned repo folder (example 'Desktop/Websites/rails-middleman-vagrant')

* Navigate to the "private_key" file in
".vagrant/machines/default/virtualbox/private_key"
and click open on this file.

* Click 'Ok' to the PuTTyGen alert window

* Click "Save Private Key"

* Click 'Yes' to the PuTTyGen alert window

* Name the .ppk file "private_key" without quotes

* Save it in the same directory as putty for organization

* Close PuTTyGen

#### To SSH in to the VM:
#### 2) SSH into Vagrant with PuTTy (This is how you will vagrant-ssh)

* Open putty.exe

##### IN SESSION:

* Set "Host Name (or IP address)" to "127.0.0.1"
* Set "Port" to "2222"
* Set "Connection Type" to "SSH"

##### IN CONNECTION/SSH/AUTH:

* Check "Display pre-authentication banner (SSH-2 only)"
* Check "Attempt authenticating using Pageant"
* Check "Attempt "keyboard-interactive" auth (SSH-2)"
* Check "Allow agent forwarding"
* Check "Allow attempted changes of username in SSH-2"
* Click Browse and navigate to the "private_key.ppk" file you
generated in the putty directory

##### IN SESSION:

* Type "vagrant" (no quotes) in the Saved Sessions input
* Click Save

To open the vagrant box from this point on you may skip the
putty setup. You will only need to open the putty.exe file and
double click "vagrant" in the saved sessions list after running
"vagrant up" in cmd or powershell.


Navigate to synced folders directory:
```terminal
$ cd /vagrant
```

#### Stop Vagrant

To suspend:
```terminal
vagrant suspend
```
To halt:
```terminal
vagrant halt
```

### -- IN CASE OF ERROR ON VAGRANT UP --

Run:
```terminal
$ lsof -i | grep LISTEN
```

If you see something listed like this:
```terminal
VBoxHeadl 4405 my_name   18u  IPv4 0xffffff802a933320      0t0  TCP *:hbci (LISTEN)
VBoxHeadl 4405 my_name   19u  IPv4 0xffffff802bcf04e0      0t0  TCP localhost:rockwell-csp2 (LISTEN)
```

Run (replace 4405 with the number in your print out):
```terminal
$ kill -9 4405
```

To check the process has been killed run:
```
$ lsof -i | grep LISTEN
```

The VBoxHeadl should be missing. You are good to now run:
```
$ vagrant up
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
$ bundle exec middleman s --port=3000
```
