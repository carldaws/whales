# (Ruby on) Whales

## Description

Whales is a bash script which creates a Dockerized Rails application, without requiring you to install Rails, Ruby, Node, Yarn, database drivers etc. The only requirement is Docker.

## Motivation & Inspiration

This project was inspired by [Docked Rails CLI](https://github.com/rails/docked) and relies on [dockerfile-rails](https://github.com/rubys/dockerfile-rails). 

Where the Docked Rails CLI allows people to get up-and-running with Rails development quickly, it is *by design* not very customisable (i.e. you can only use the Rails defaults). On the other hand, the goal of dockerfile-rails is to be able to generate Dockerfiles for any Rails project.

Whales brings these two ideas together. With Whales, you can get set up with a relatively custom Dockerized Rails application, in just a few commands, without needing to install anything other than Docker. 

Whales allows you to create a new Rails application with all of the options of the `rails new` command, and Dockerizes it for easy development and deployment. 

## How to use this script

1. Download the script:

```
curl -so whales https://raw.githubusercontent.com/cdwsn/whales/main/whales && chmod +x whales && alias whales=./whales
```

2. Generate a new application:

```
whales new weblog -d=postgresql -j=esbuild
cd weblog
```

3. Create the database, generate a scaffold, run a migration:

```
whales rails db:create
whales rails g scaffold post title:string body:text
whales rails db:migrate
```

4. Start the container(s):

```
whales up
```

(Note: if you'd like the `whales` command to always be available in your terminal, instead of `./whales`, you'll have to add the alias to your terminal profile)

## Command List

`whales new`: Generate a new Dockerized Rails app

`whales compose`: Run any `docker compose` command in the development environment

`whales up`: Start the containers for the development environment (using the bin/dev script if using css or js bundling)

`whales down`: Stop the development containers

`whales build`: Build the development containers as specified by the docker-compose file

`whales bash`: Start a shell session in the web / Rails service (requires the container to be running, which can be done with `whales up`)

`whales run`: Execute a single `docker compose run` command against a service, and remove the container when finished

`whales recompose`: Regenerate the development docker-compose file (to be used after regenerating the Dockerfile using `rails generate dockerfile --compose`)

`whales rails`: Execute a single `rails` command against the web / Rails service, and remove the container when finished

`whales bundle`: Executes a single `bundle` command against the web / Rails service, and remove the container when finished

`whales rspec`: Executes the equivalent of a `bundle exec rspec` command (requires you to install the rspec-rails gem and run `whales rails g rspec:install` first)