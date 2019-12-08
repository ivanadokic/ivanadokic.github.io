---
layout: post
title:      "The New York Park - CLI"
date:       2019-12-08 17:38:37 -0500
permalink:  the_new_york_park_-_cli
---


The New York City Park CLI ( Command Line Application) would scrape [NYC Parks](https://www.nycgovparks.org/) website, to give the user data about different Parks in the selected NYC zip code area. Its build in Ruby, dynamic, open source programming language that's  been used to build some of the awesome sites apps we use each day, like Twitter, Groupon, GitHub, Hulu, Square and Shopify.  

Not all of the data we might be interested in using to program is available to use through APIs. 

With Web scraping we are no longer limited to working with APIs and publicly available data sources.

[Ruby](https://www.ruby-lang.org/en) developers use Nokogiri gem as an essential web scraping tool. When combined with OpenURI, a native Ruby library for easily accessing web pages, it becomes a powerful way to get information from websites which otherwise don’t make data available through an API or RSS feed.

<a href="https://imgur.com/HYEi8db"><img src="https://i.imgur.com/HYEi8dbl.png" title="source: imgur.com" /></a>

### So what is Nokogiri? 
[Nokogiri](https://nokogiri.org/) is an open source software library to parse HTML and XML in Ruby. It’s actually a ruby gem that will transform a webpage into a ruby object and make all of this web scraping stuff really easy. And ruby gems are optional add-on libraries of code so developers don’t have to reinvent the wheel each time the app with a common use case is build.

**STEP 1**
INSTALL NOKOGIRI

The first thing you need to do to use Nokogiri is to install it. You can do so in your terminal with the following code:

`gem install nokogiri`

**STEP 2**
OPENING a Web Page as HTML with Nokogiri and open-uri

Let's say we have a file, scraper.rb which is responsible for scraping. We need to require Nokogiri and open-uri:

```
require 'nokogiri'
```

```
require 'open-uri'
```

**STEP 3**
NOKOGIRI & CSS SELECTORS

CSS-Cascading Style Sheets - describe how HTML elements are to be displayed on screen, paper, or in other media.
To scrape you will need to select an element. To select an element simply pass the name of the element you want into the Nokogiri document object’s CSS method.
### How to Choose a CSS Selector 
In the following steps i'll show how do we determine which selector to use to retrieve the desired information.
##### FIGURE OUT WHAT YOU WANT TO SCRAPE

Start by figuring out what information you want to scrape. Use the element inspector to find the selector of a certain piece of HTML. In this case, we'll look the element containing the text in **Facilities **section.

##### This is one of the pages I used for NYC Park CLI 

<a href="https://imgur.com/4xJCSyB"><img src="https://i.imgur.com/4xJCSyBl.png" title="source: imgur.com" /></a> 


Hover over an example of the item you’re looking for and with Right click on hit Inspect. 

This will highlight the corresponding CSS in the Elements window while highlighting the element’s bounds (usually through a colored box). 

Click on the item to select its CSS in the Elements window and with Right click on hit Copy and than Copy Selector


<a href="https://imgur.com/LpwKOBg"><img src="https://i.imgur.com/LpwKOBgl.png" title="source: imgur.com" /></a>


Nokogiri collects these objects into a hierarchical data structure and allows us to iterate over an array of Nokogiri objects and use enumerators to grab the values of attributes and text.

#### `array_of_facilities = doc.css("span.park_facilities_list_text")`


<a href="https://imgur.com/c4gLX3e"><img src="https://i.imgur.com/c4gLX3el.png" title="source: imgur.com" /></a>

#### Conclusion
By using Nokogiri, we can get any website's HTML, represented in XML objects, including any text or data displayed on that site. 

Scraping require customized code for each site we want to scrape as each website is designed differently.

However, being able to scrape websites gives us access to information that can be time-consuming or otherwise very difficult to collect. 


