---
layout: post
title:      "Sinatra MVC File Structure"
date:       2020-01-05 18:32:03 -0500
permalink:  sinatra_mvc_file_structure
---


<a href="https://imgur.com/0Z6MxPf"><img src="https://i.imgur.com/0Z6MxPfl.jpg" title="source: imgur.com" /></a>

[Sinatra](http://sinatrarb.com/) is a Domain Specific Language (DSL) for creating web applications in Ruby. It is dependent on the Rack web server interface. 

Companies that use Sinatara include Apple, BBC, GitHub, LinkedIn, National Security Agency, Heroku and many more.

Working with Sinatra allows you to dive in deep with the major concepts of MVC (Models-Views-Controllers), a system for building web applications that governs majority of the worlds' apps. 

MVC is a pattern for the architecture of a software application. It separates an application into the following components:
* Models for handling data and business logic
* Controllers for handling the user interface and application
* Views for handling graphical user interface objects and presentation

## Models, views and controllers of the MVC framework
The Models, Views and Controllers will be grouped into a folder named **app directory** where we spend most of our time coding. All the main files are organized inside an app folder with subfolders corresponding to each component of MVC: **models** for object model files,****  views  ****for html template files, and **controllers** for controller files.
<a href="https://imgur.com/3Vnt72p"><img src="https://i.imgur.com/3Vnt72pl.png" title="source: imgur.com" /></a>
### models directory
This directory holds the logic behind our application. Typically, these files represent either a component of our application, such as a User, Post, or Comment... Each file in models typically contains a different class. 

In Sinatra, models are generally written as Ruby classes. 

For example, dog.rb would contain a class called Dog and have name, breed, and age attributes which can be set on initialization. We should be able to read and write to these attributes and this class should also keep track of each instance of dog created, as well as a class method all to return an array of those instances: 
```
class Dog
    attr_accessor :name, :breed, :age
    @@all =[]
    def initialize (name, breed, age)
        @name = name
        @breed = breed
        @age = age
        self.class.all << self
    end
    def self.all
        @@all
    end  
end
```
### controllers directory
The controllers, such as application_controller.rb, are where the application configurations, routes, and controller actions are implemented. Controllers represent the application logic, generally; the interface and flow of our application. There is typically a class, in this case we will call it ApplicationController, that represents an instance of our application when the server is up and running. The application_controller.rb file represents the "C" components of the MVC paradigm.

In Sinatra, controllers are written in Ruby and consist of 'routes' that take requests sent from the browser ("GET this data", "POST that data"), run code based on those requests by using models, and then render the .erb (view) files for the user to see. We've created a controller action that can receive and respond to a GET request to the root URL '/'. This GET request loads the index.erb file.
```
class ApplicationController < Sinatra::Base
  configure do
  	set :views, "app/views"
  	set :public_dir, "public"
  end
  get "/" do
  	erb :index
  end
end

```
### views directory
This directory holds the code that will be displayed in the browser. By convention, our file names will match up with the action that renders them. For example, a GET request to / typically renders a file called index.erb.

In Sinatra, views are written as .erb files, consisting of HTML and embedded Ruby (Ruby code written within HTML). They are what the user actually sees when they use your web application. We created a file called index.erb inside of the views directory with the following code: 
```
 <!DOCTYPE html>
<html>
  <head>
    <title>Sinatra MVC</title>
  </head>
  <body>
    <h1>Frank Sinatra Greatest Hits</h1>
    <img src="https://i.imgur.com/fW7jh7pl.jpg">
  </body>
</html>
 ```

We've already told the controller how to load this file in the view. 
### How things look and are displayed in our application
To test our app we used Shotgun - Ruby gem that makes it easier to develop and test Rack-based Ruby web applications locally by starting Rack with automatic code reloading. 

After we run `shotgun` to start a local server and test our app in browser, this is how things are displayed: 


<a href="https://imgur.com/tAlg29y"><img src="https://i.imgur.com/tAlg29yl.png" title="source: imgur.com" /></a>

