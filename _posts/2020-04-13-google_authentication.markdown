---
layout: post
title:      "Google Authentication"
date:       2020-04-13 23:44:42 +0000
permalink:  google_authentication
---


[OmniAuth](https://github.com/omniauth/omniauth) is a gem for Rails that lets you use multiple authentication providers alongside the more traditional username/password setup. It supports many authentication providers: Facebook, LinkedIn, GitHub full list can be found [here](https://github.com/omniauth/omniauth/wiki/List-of-Strategies). 
## Here's how OmniAuth works from the user's standpoint:
1. User tries to access a page on **yoursite** that requires them to be logged in. They are redirected to the login screen.
2. The login screen offers the options of creating an account or logging in with Google.
3. The user clicks Log in with Google. This momentarily sends the user to **yoursite.com/auth/google**, which quickly redirects to the Google sign-in page.
4. If the user is not already signed in to Google, they sign in normally. More likely, they are already signed in, so Google simply asks if it's okay to let yoursite.com access the user's information. The user agrees.
5. They are (hopefully quickly) redirected to **yoursite.com/auth/google/callback** and, from there, to the page they initially tried to access.


<a href="https://imgur.com/MMPRGi0"><img src="https://i.imgur.com/MMPRGi0h.png" title="source: imgur.com" /></a>

### Installation
Add to your Gemfile:
```
gem 'omniauth-google-oauth2'
```
Then `bundle instal`

Go to https://console.developers.google.com and login with your google account.
Click on select a project

Click on Credentials and click on the “OAuth consent screen” tab to set up
You require the client ID and client secret for your rails app

### Middleware
Add the middleware to the project in config/initializers/omniauth.rb.
```
Rails.application.config.middleware.use OmniAuth::Builder do
    provider :google_oauth2, ENV["GOOGLE_CLIENT"],ENV["GOOGLE_SECRET"], skip_jwt: true
  end
```
You can now visit the url:/auth/google_oauth2 to assess the google authentication.

### Routes
Routes for Google authentication, expect callback from server 

 `get '/auth/:provider/callback' => 'sessions#omniauth'` 
 
 ### Controller
 
Uid ensures its unique instance that we havent had before 
 
 ```
def omniauth
    @player = Player.find_or_create_by(uid: auth[:uid]) do |p|  
     p.username =auth[:info][:name] 
     p.age = 11
     p.password = SecureRandom.hex #give us random password 
  end
    @player.assign_team
  
    session[:player_id] = @player.id
    redirect_to root_path
end

private
def auth
    request.env['omniauth.auth']
end
````
### Migration
In the migration add:

```
class AddColumnToPlayers < ActiveRecord::Migration[6.0]
  def change
    add_column :players, :uid, :string
  end
end

```


<a href="https://imgur.com/LhjYU6E"><img src="https://i.imgur.com/LhjYU6El.jpg" title="source: imgur.com" /></a>




