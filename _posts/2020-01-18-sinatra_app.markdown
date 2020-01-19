---
layout: post
title:      "Sinatra app "
date:       2020-01-18 23:27:25 -0500
permalink:  sinatra_app
---

Shoes MVC web app project was build in a Sinatra using Active Record. This is a custom app created to track shoes. Basically it’s a simple Content Management System (CMS). The requirements included:

1. Build an MVC Sinatra app
2. Use ActiveRecord with Sinatra&#x2028;
3. Use multiple models&#x2028;
4. Use at least one has_many relationship on a User model and one belongs_to relationship on another model.&#x2028;
5. Users must be able to sign up, sign in, and log out.
6. Validate Uniqueness of user login attribute (username or email).&#x2028;
7. Once logged in, a user must have the ability to create, read, update and destroy the resource that belong_to the user.&#x2028;
8. Users can edit and delete only their own resources.&#x2028;
9. Validate user input so bad data cannot be persisted to the database.&#x2028;

(<a href="https://imgur.com/4diC8jN"><img src="https://i.imgur.com/4diC8jNl.png" title="source: imgur.com" /></a>

## Structure the MVC - Corneal gem 

I started with [Corneal](https://thebrianemory.github.io/corneal/ ) gem which sets up the file structure for a Sinatra MVC application for you. Its a helpful tool that can ease the structuring process of the Model Views Controller,  cool gem called corneal. You only need to install the gem by `gem install corneal` and run `corneal new APP-NAME` to generate your app. Then, run `bundle install ` to install all missing gems. 

## Models:
There are two models: a shoe and a user. A clas Shoe has category, size and brand and belongs to user, a clas User has username, email and password and has_many shoes and classes both inherits from ActiveRecord::Base
```
class Shoe < ActiveRecord::Base
    belongs_to :user
end
```
I was able to validate the uniqueness of the user’s email address by adding the ActiveRecord validate prompt to the user class. This ActiveRecord macro gives us access to a few new methods. A macro is a method that when called, creates methods for you, using a macro is just like calling a normal ruby method. In this case, the macro has_secure_password is being called just like a normal ruby method. It works in conjunction with a gem called bcrypt and gives us all of those abilities in a secure way that doesn't actually store the plain text password in the database.



```
class User < ActiveRecord::Base
    has_many :shoes
    has_secure_password 
end
```
## Migration Overview:

Migrations are a convenient way to alter database schema over time in a consistent and easy way. They use a Ruby DSL so that you don't have to write SQL by hand, allowing your schema and changes to be database independent. Each migration is kind of a new 'version' of the database as schema starts off with nothing in it, and each migration modifies it to add or remove tables, columns, or entries. Active Record knows how to update your schema along this timeline, bringing it from whatever point it is in the history to the latest version. 

Here's an example of a migration and schema: 

```
class CreateShoes < ActiveRecord::Migration
  def change
    create_table :shoes do |t|
      t.string :category
      t.integer :size
      t.string :brand
      t.integer :user_id

      t.timestamps null: false
    end
  end
end
```
```
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.string :password_digest 
    end
  end
end
```
```
ActiveRecord::Schema.define(version: 20200114144725) do

  create_table "shoes", force: :cascade do |t|
    t.string   "category"
    t.integer  "size"
    t.string   "brand"
    t.integer  "user_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "email"
    t.string "password_digest"
  end

end
```

## Password Encryption with BCrypt
BCrypt will store a salted, hashed version of our users' passwords in our database in a column called **password_digest**. Essentially, once a password is salted and hashed, there is no way for anyone to decode it. This method requires that hackers use a 'brute force' approach to gain access to someone's account –– still possible, but more difficult.

Watch the development process on YouTube, or view the source on GitHub.





