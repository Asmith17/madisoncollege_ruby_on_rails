#Ruby on Rails Development
##Week 2

----
#Agenda 
* Terminology
* Generating a new Rails application
  * Gems
  * Bundler
* Git
* Heroku

---
#Chapter 1

---
#What is Ruby?

> A dynamic, open source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.

---
#What is Rails
> Ruby on Rails is an open-source web framework that's optimized for programmer happiness and sustainable productivity.

---
#Ruby version Managers
* Tools to allow you to install several versions of Ruby side by side
* Popular ones are: RVM, rbenv and chruby.

---
#What are Gems (RubyGems)?
>RubyGems is a package manager for the Ruby programming language that provides a standard format for distributing Ruby programs and libraries (in a self-contained format called a "gem"), a tool designed to easily manage the installation of gems, and a server for distributing them.

---
#The Gem command
* ```$ man gem```
* ```$ gem install <gem name> -v=<gem version>```
* ```$ gem list````
* ```$ gem uninstall <gem name>```

---
#Configuration Files
##AKA 'Dot' files

---
#Dot Files
* Start with a ```.``` so they are 'hidden'
* Can be used to configure many applications

---
#.gemrc
```
install: --no-rdoc --no-ri
update:  --no-rdoc --no-ri
```
* This says don't install ri or rdoc when installing a gem
* If you *need* docs locally remove these

---
#```$ rails new```

---
```
$ rails new first_app
      create
      create  README.rdoc
      create  Rakefile
      create  config.ru
      create  .gitignore
      create  Gemfile
      create  app
      create  app/assets/javascripts/application.js
      create  app/assets/stylesheets/application.css
      create  app/controllers/application_controller.rb
      .
      .
      .
      create  vendor/assets/stylesheets/.keep
         run  bundle install
```

---
#Let's explore what files are generated
---
#Instructor opinion
Add the ```--skip-bundle``` flag at the end of your generation command.  It allows your app to be generated and you to make changes before installing gems.

---
#Bundler
>Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as ```bundle install```.

---
#Bundler
Makes use of two files:
* Gemfile
* Gemfile.lock

---
#Gemfile
* A list of all your application's required Gems
* Bundler uses this to manage which Gems to load
* [http://bundler.io/v1.2/man/gemfile.5.html](http://bundler.io/v1.2/man/gemfile.5.html)
* Allows you to group gems for what they are used for ie. Test, Development, Production

---
##Gemfile.lock
* A snapshot from when you run bundle install.  
* Not the best idea to modify by hand!

---
#Bundler
* ```$ bundle help```
* ```$ bundle install``` installs gems
* ```$ bundle check``` checks to see if Gemfile is satisfied
* [http://bundler.io/v1.7/commands.html](http://bundler.io/v1.7/commands.html)

---
#Rails server
* ```$ bundle exec rails server ```

> on cloud 9 add ```-b $IP -p $PORT```

---
#MVC

---
![fit](https://dl.dropboxusercontent.com/s/gkvmxepquu061xc/2014-09-06%20at%2012.48%20PM.png?dl=0)

---
##Model
* Responsible for maintaining the state of the application
* Enforcing business rules

---
##View
* User interface

---
##Controller
* Orchestrate the application (Traffic Cop)

---
#What is REST?
> Representational State Transfer 

* Simple set of Verbs that work on each Noun of an application.

--- 
#What is a 'resource'?
* Simply a controller 
* Scaffolding creates a 1 to 1 relationship to model
* Does not need to reflect a model 
* Defaults to REST actions

---
#What is 'scaffolding'
* Generated by the ```scaffold``` command
* Generates code based on the attribute notation ```name:string```
* Creates model, view, controller, helper, route, migration and tests
* Has default basic code

---
#Example Route

```
DemoApp::Application.routes.draw do
  resources :users
end
```

---
#$ rake routes

```
Prefix    Verb   URI Pattern                    Controller#Action
users     GET    /users(.:format)               users#index
          POST   /users(.:format)               users#create
new_user  GET    /users/new(.:format)           users#new
edit_user GET    /users/:id/edit(.:format)      users#edit
users     GET    /users/:id(.:format)           users#show
          PATCH  /users/:id(.:format)           users#update
          PUT    /users/:id(.:format)           users#update
          DELETE /users/:id(.:format)           users#destroy
```
^Maps to CRUD actions (index,show,new,create,edit,update,destroy)

---
##PUT vs PATCH
* PATCH is like PUT however PUT works on the full dataset where as PATCH only requires the delta.
* PATCH was defined in 1995 and adopted into Rails in version 4.0

---
##Sample update request
```
started PATCH "/users/1" for 50.50.89.28 at 2014-12-26 12:22:13 +0000
Processing by UsersController#update as HTML
  Parameters: {"utf8"=>"✓", "authenticity_token"=>"dWzrsueQQJPL9PxuZnM8NnQYzrtC34PpV6sbK8bd0oaxzLHlgK0224q+OVWrDF
  /HApdIAZGy2ywGlzQ0oywpAQ==", "user"=>{"name"=>"chris", "email"=>"cgjohnson1@madisoncollege.edu"}, "commit"=>"Update User", "id"=>"1"}
  User Load (0.2ms)  SELECT  "users".* FROM "users" WHERE "users"."id" = ? LIMIT 1  [["id", 1]]
   (0.1ms)  begin transaction
  SQL (0.4ms)  UPDATE "users" SET "name" = ?, "updated_at" = ? WHERE "users"."id" = ?  [["name", "chris"], 
  ["updated_at", "2014-12-26 12:22:13.298574"], ["id", 1]]
   (29.2ms)  commit transaction
Redirected to http://grandeur-blackwater-bay-69-123648.use1.nitrousbox.com:3000/users/1
Completed 302 Found in 36ms (ActiveRecord: 29.8ms)
```

---
##Modeling demo users

![inline 200%](https://softcover.s3.amazonaws.com/636/ruby_on_rails_tutorial/images/figures/demo_user_model.png)

--- 
##Modeling demo microposts 

![inline 200%](https://softcover.s3.amazonaws.com/636/ruby_on_rails_tutorial/images/figures/demo_micropost_model.png)

---
#Rake
* Ruby make

##Protip
```$ bundle exec rake -vT```

---
#Let's take a tour

---
#Preparing for the demo today

* Note: make sure you have removed 'wolfies_list' if you generated one last week.
* ```$ git clone git@github.com:johnsonch/wolfies_list.git ```
* ```$ cd wolfies_list```
* ```$ bundle install --path=vendor/bundle```

---
#What are we building?
##Wolfie's List

![inline fit](https://s3.amazonaws.com/uploads.hipchat.com/14021/49351/LX1s86FC722Tzy6/wolfieslist.png)


---
#Demo

^ Clean up Heroku messes
- delete from heroko
- remove from git config
- ```$ heroku create```

^ Scaffold ads
```
$ bundle exec rails g scaffold Ads title:string description:text price:float address:string
```
Scaffold categories
```
$ bundle exec rails g scaffold Categories name:string 
```
Add relationship
- generate migration ```bundle exec rails g migration add_category_id_to_ads```
- add relationships to models
  
---
#Active Record Relationships

---
##Active Record Relationships
* belongs_to
* has_many
* has_many_through

---
##Validations
* Rules to prevent invalid data from being saved
* Can be conditional
* Provides error messages back to the controller
* [http://guides.rubyonrails.org/active_record_validations.html#validation-helpers](http://guides.rubyonrails.org/active_record_validations.html#validation-helpers)

---
##Rails Console
* Let's you try out code against 
* ```$ bundle exec rails console```

---
#Rails Class Inheritance Hierarchies

[https://www.railstutorial.org/book/toy_app#sec-inheritance_hierarchies](https://www.railstutorial.org/book/toy_app#sec-inheritance_hierarchies)
#Git

--
##Configuring Git
* See what is in your git config file ```cat ~/.gitconfig```
```
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com
```
* ```cat ~/.gitconfig```

---
#Git Demo
^
```
$ mkdir class_git_demo
$ cd class_git_demo
$ git init
$ touch file-a.txt
$ git status
$ git add file-a.txt
$ git status
$ git commit -a -m 'our first file'
$ git status
$ git log
$ git checkout -b branch-a
$ touch file-branch-a.txt
$ git status
$ git add .
$ git commit -am 'branch-a file added'
$ git log
$ git checkout master
$ git merge branch-a
$ git branch --contains <sha>
$ git branch -d branch-a
$ git checkout -b branch-b
$ touch file-branch-b.txt
$ git add .
$ git commit -am 'added file-branch-b'
$ vim file-branch-b.txt
$ git status
$ git diff
$ git add .
$ git commit -am 'added Hello World to file-branch-b'
$ git log
$ git checkout -b branch-c
$ touch file-branch-c.txt
$ git add .
$ git commit -am 'added file-branch-c.txt'
$ vim file-branch-c.txt
$ git add .
$ git commit -am 'added code to branch-c file'
$ vim file-branch-c.txt
$ vim file-branch-a.txt
$ git status
$ git diff
$ git add .
$ git commit -am 'edits to both a and c'
$ git tree
$ gco master
$ git merge branch-c
$ git status
$ git tree
$ vim ~/.gitconfig
  add ```  tree = log --graph --decorate --oneline --all --color ```
$ git tag
$ git status
$ git tag -a project-1 -m 'my code for project 1'
$ git tag
* $ git push --tags
```

---
#Github
* Creating a repository
* Inviting contributors

---
#Deploying

---
#Heroku vs VPS

---
##Heroku
* Managed
* $$
* Step 1: ```$ heroku create my-sweet-app```
* Step 2: ```$ git push heroku master```
* Step 3: Profit!

---
##VPS
* Owned by you
* Many deployment options
* $
---
Ruby Koans
* Let's see how to install and work on them

---
##Next Week
* Chapter 4
* Attempt Lab 3  
* Lab 1 due by Wednesday night at 11:55pm
