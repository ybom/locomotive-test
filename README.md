Build CMS demo with Rails

## LocomotiveCMS-Rails setup

### Ubuntu
```
sudo apt-get update
sudo apt-get install git
```

### RMV install
```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io | bash -s stable
source /home/vagrant/.rvm/scripts/rvm
```

### Ruby install with [rvm](https://rvm.io/rvm/install)
```
rvm install 2.4.1
rvm use 2.4.1 --default (set default version globally)
```

### Install DB
```
MongoDB
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo service mongod start
mongo
use admin
db.createUser({user:"admin", pwd:"123", roles:[{role:"root", db:"admin"}]})
vim /lib/systemd/system/mongod.service
```
* Follow the rest of these steps: https://thecustomizewindows.com/2017/11/how-to-install-configure-secure-mongodb-on-ubuntu-16-04-lts/
* After restart
```
mongo -u admin -p 123 --authenticationDatabase admin
use db_name
db.createUser({user:"admin", pwd:"123", roles:[{role:"readWrite", db:"db_name"}]});
```

### Install ImageMagick
`sudo apt-get install imagemagick`

### Install LocomotiveCMS
```
rails new locomotive-test --skip-bundle --skip-active-record
Add gem 'locomotivecms', '~> 3.3’ to Gemfile
bundle install
run bundle install again
```
The Locomotive Engine has been correctly installed in your Rails application.

  1. Edit the main config files:

    - config/initializers/carrierwave.rb
    - config/initializers/devise.rb
    - config/initializers/dragonfly.rb
    - config/initializers/locomotive.rb
    - config/devise.yml
    - config/mongoid.yml
    - config/routes.rb
to run it
`rails s -b0.0.0.0` because by default rails4.2 is running on localhost
