---
layout: post
title:      "RESTful Conventions in Rails"
date:       2020-02-16 20:21:12 -0500
permalink:  restful_conventions_in_rails
---


## What is REST?

By definition Representational state transfer (REST) is a software architectural style that defines a set of constraints to be used for creating Web services.  REST was defined by Roy Fielding in his 2000 PhD dissertation. It’s a standard way web apps should structure their URLs. It provides a way of mapping HTTP verbs ( get, post, put, delete) and CRUD actions (create, read, update, delete) together.

[Rails](https://rubyonrails.org/) has RESTful principles built into its core. There are seven RESTful route options available, that match the HTTP verbs and allow us to perform CRUD (Create, Read, Update, Delete) actions. Routes are the code that are responsible for listening and receiving requests and then deciding what to send back. The routes we’ll start with will allow us to gather data and present it: 

1. Index
2. New
3. Create
4. Show

The last 3 routes will mutate that data:

5. Edit
6. Update
7. Destroy

RESTful routes have a clear mapping between the URL resource and the corresponding controller actions. Here is a mapping of all of the different route helpers, HTTP verbs, paths, and controller action mappings: 

<a href="https://imgur.com/omB0PMx"><img src="https://i.imgur.com/omB0PMxl.png" title="source: imgur.com" /></a>


> The beauty of following these conventions is that you don’t have to reinvent the wheel every time you build a new CRUD app, the routes and method names have already been decided.
> 

Connect with Me on [Twitter](https://twitter.com/LloydPile) or  [LinkedIn](https://www.linkedin.com/in/ivana-dokic-b96460120/)


