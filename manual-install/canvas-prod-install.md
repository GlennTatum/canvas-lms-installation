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

- Description:

In the Canvas production install guide Canvas already has
template YAML files for configuration in place.
These template placement scripts do not have to be ran
if the location of the files are known and the content
of the files are known. With this in mind the Ansible configuration
should contain the template variables so that the config files
can be easily placed into their required directories.


