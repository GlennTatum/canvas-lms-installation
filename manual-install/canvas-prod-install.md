Pre setup Notes:

Check if Ubuntu has required Ruby Versions (2.7)

Check if Ubuntu has required Node.js Versions (14.x LTS)

Check if Ubuntu has required npm Versions

Check if Ubuntu has required Yarn Versions (1.19.1-1)

This alleiviates the need to add more external
ppa's and repositories.

### Cloud Init Notes

Packages: software-properties-commmon git

### Setup Canvas Enviornment

IMPORTANT: The root directory canvas will be setup
in this instllation will be /var/canvas/

cd /var/

git clone https://github.com/instructure/canvas-lms.git canvas

cd canvas

git checkout prod

OR

Install Canvas Production through tar or zip

### Install Dependincies

- PPA

(Ruby) sudo add-apt-repository ppa:brightbox/ruby-ng

(Redis) sudo add-apt-repository ppa:chris-lea/redis-server

- Repositories

(Yarn GPG Key) curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -

(Yarn) echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

- Custom Reposiories

(Nodejs) curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -

- Dependincies

(Repo Management) sudo apt-get install software-properties-common - Already done in Cloud-init

(Git) sudo apt-get install git-core - Already done in Cloud-init

(Python) sudo apt-get install python

(Apache Web Server) sudo apt-get install passenger libapache2-mod-passenger apache2

(Redis)  sudo apt-get install redis-server

(Postgres) sudo apt-get install postgresql-12

(Nodejs) sudo apt-get install nodejs

(Nodejs - NPM) sudo npm install -g npm@lates

(Yarn) sudo apt-get install yarn=1.19.1-1

(Yarn Deps) sudo yarn install

(Dev Tools-Ruby) sudo apt-get install ruby2.7 ruby2.7-dev zlib1g-dev libxml2-dev libsqlite3-dev postgresql libpq-dev libxmlsec1-dev curl make g++

(Ruby - Gems) sudo gem install bundler --version 2.2.19

(Ruby - Bundler) sudo bundle _2.2.19_ install --path vendor/bundle

### Configure Canvas Enviornment

---

## Canvas Config files

- Description:

In the Canvas production install guide Canvas already has
template YAML files for configuration in place.
These template placement scripts do not have to be ran
if the location of the files are known and the content
of the files are known. With this in mind the Ansible configuration
should contain the template variables so that the config files
can be easily placed into their required directories.

- Canvas Base Configuration files:

amazon_s3.yml
delayed_jobs.yml
domain.yml
file_store.yml
outgoing_mail.yml
security.yml
external_migration.yml
dynamic_settings.yml
database.yml

Note: All configuration files will be located
and place into the /canvas/config directory. The
configuration file variables will be setup through
the Ansible Playbook.

## Static Assets

- Generate Canvas Static Assets:

https://github.com/instructure/canvas-lms/wiki/Production-Start#generate-assets


## PostgreSQL setup

- PostgreSQL database population

(Manual Config) RAILS_ENV=production bundle exec rake db:initial_setup

Note: PostgreSQL tables will be setup through
the Ansible playbook.


## Apache Web Server

1. Disable any exsisting Apache web server virtualhosts
that are not required.

sudo unlink /etc/apache2/sites-enabled/000-default.conf

2. Create an Apache web server virtualhost for Canvas.

sudo nano /etc/apache2/sites-available/canvas.conf

3. Configure variables in the canvas.conf file created

Apache configuration Variables:

ServerName (Domain Name)
Server Alias (Regular name such as "canvas")
ServerAdmin (Admin Email)
DocumentRoot ({var, home, etc...}/canvas/public)
SetEnv (Production or Dev setup)
Directory ({var, home, etc...}/canvas/public)

Note: This will be setup for Port 80 and Port
443 virtualhosts for SSL.

Note: The apache webserver and the configurations
required variables will be set through the Ansible
Playbook.


- Passenger Troubleshooting:

https://github.com/instructure/canvas-lms/wiki/Production-Start#configure-passenger-with-apache

Note: If the passenger installation went correctly
the rest of these steps are for troubleshooting.
None of these commands have to be done if the file
symlinks are in place or if the canvas user on the system can
not start the apache web server.

### Canvas automated job daemon configuration

Steps to setup the Canvas automated job daemon:

https://github.com/instructure/canvas-lms/wiki/Production-Start#installation-1

### Start the Canvas-lms server

sudo /etc/init.d/apache2 restart



