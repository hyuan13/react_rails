# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version: \
    ruby-2.5.5
* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

This guide shows you how to use Docker Compose to get the application up and run a Rails/PostgreSQL/Webpacker/React app on Ubuntu 18.04.

* Download react_rails into your local directory.
```
git clone https://github.com/hyuan13/react_rails.git
```
* cd into working directory.
```
cd react_rails
cd test_app
```
* Manually delete node_modules and yarn.lock
* Set up the files needed to build the app. App will run inside a Docker container containing its dependencies. Defining dependencies is done using a file called Dockerfile.
```
docker-compose build
```
* Use Bundler to manage your ruby on rails application's dependencies by installing all the required gems.
```
docker-compose run web bundle install
```
* Install all the dependencies listed within package.json in the local node_modules folder.
```
docker-compose run web yarn install
```
* Create the database
```
docker-compose run web rake db:create
```
* Database migration
```
docker-compose run web rake db:migrate
```
* Populate the database with seed.rb
```
docker-compose run web rake db:seed
```
* Boot the app
```
docker-compose up
```


