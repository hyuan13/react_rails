# README

Things you may want to know.

* Ruby version: \
    ruby-2.5.5
* Node version: \
    v12.4.0
* Services: \
    postgress db \
    webpacker \
    web

This guide shows you how to use Docker Compose to get the application up and run a **Rails/PostgreSQL/Webpacker/React** app on Ubuntu 18.04.

* Download react_rails into your local directory.
```
git clone https://github.com/hyuan13/react_rails.git
```
* cd into working directory.
```
cd react_rails
cd test_app
```
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

Tips you may want to know.

* Invoke the postgres console from the command line
```
docker-compose run web rails c
```
* View table contents in schema.rb in postgres console
```
tablename.all
```
* Delete table contents in schema.rb in postgres console
```
tablename.delete_all
```
* Create new database schema in docker
```
docker-compose run web rails g model tablename parameter1:type parameter2:type
```
* List all docker images
```
docker images -a
```
* Remove all docker images
```
docker rmi -f $(docker images -a -q)
```
* List all docker containers
```
docker ps -a
```
* Remove all docker containers
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
* List all docker volumes
```
docker volume ls
```
* Remove all  docker volumes
```
docker volume prune
```
* Precompile all the assets
```
docker-compose run web bundle exec rake assets:precompile
```

Rebuild the application.
* If you make changes to the Gemfile
```
docker-compose run web bundle install
docker-compose build
```
* If you make changes to the package.json
```
docker-compose run web yarn install
docker-compose build
```

Deployment instructions
