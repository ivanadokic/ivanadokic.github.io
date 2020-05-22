---
layout: post
title:      "Java srcipt app - Book Reviews"
date:       2020-05-16 20:34:24 -0400
permalink:  java_srcipt_app_-_book_reviews
---


Due to the Covid-19, the stay-at-home orders for millions of people across the world have radically changed how we spend our time. One activity that’s been largely untouched by the pandemic is Reading. What is on your reading list and option to share your favorite titles and add reviews, anything a potential reader should know about such as "Beautiful writing" or "great pricing" were used as a user story and a features on Book reviews application. 

Ultimate goal, build Book reviews single page application (SPA) using a JavaScript frontend and a Rails API backend was set.

During the Covid-19 pandemic as many other parents, my new normal became filled with google classrooms and spreadsheets, zoom calls, kids' online worksheets, checking their writing and helping them log onto google hangouts, turn in assignments and using many different platforms. Some of them like PEARSON REALIZE - newest learning management system, than IReady, MyON, iXL Science, Flipgrid really required my involvement.

<a href="https://imgur.com/weFiLwg"><img src="https://i.imgur.com/weFiLwgh.jpg" title="source: imgur.com" /></a>

And with all this “new normalcy”, building Book reviews application was not an easy task but i decided to use whatever time I can find to start working on a this project and incorporate many of the new skills I was hoping to learn but this time with limited time due to three kids homescholing. 

> This required new approaches and mentorship.

> Thanks to Noah Pryer, CTO at [TEACHABLE ](https://teachable.com/) all-in-one platform that helps you create and sell courses online, and handles everything from web hosting to payment processing, I was able to complete this project and create Book reviews application. His extensive professional and academic knowledge was support needed during this period.

**Project Requirements**
* HTML, CSS, and JavaScript frontend with a Rails API backend. All interactions between the client and the server required to be handled asynchronously (AJAX) and use JSON as the communication format. 
* It needed to organize data through Object Oriented JavaScript (classes) to encapsulate related data and behavior, and domain model served by the Rails backend must include a resource with at least one has-many relationship. 
* The backend and frontend must collaborate to demonstrate Client-Server Communication. 
* Application should have at least 3 AJAX calls, covering at least 2 of Create, Read, Update, and Delete (CRUD). 
* Client-side JavaScript code must use fetch with the appropriate HTTP verb, and your Rails API should use RESTful conventions.

**Language and skills implemented**

Project was build using a Rails API for the backend and JavaScript for the frontend. Toolset included Visual Studio Code (editor/terminal), GitHub and Postgres for database.

## **Rails API Backend**

The Rails component of this project is very straightforward with a Book and Review models and associactions.

**Setting up:**

**Models**
```
class Book < ApplicationRecord
    has_many :reviews
end
```
```
class Review < ApplicationRecord
    belongs_to :book
end
```
**Controllers**
```
class BooksController < ApplicationController

    # GET /books
    def index
        books = Book.all 
        options = {}
        options[:include] = [:reviews]
        render json: BookSerializer.new(books, options)
    end
    def show
        book = Book.find_by(id: params[:id])
        render json: BookSerializer.new(book)
    end
    # POST /books
    def create
        
        new_book = Book.new(book_params)
        if new_book.save
            render json: BookSerializer.new(new_book)
        else
            render json: new_book.errors
        end
    end
   
    def destroy
        book = Book.find_by(id: params[:id])
        book.destroy
    end

    private

    def book_params
        params.require(:book).permit(:title, :author, :genre, :image_url)
    end
end

```


```
class ReviewsController < ApplicationController
  def index
    reviews = Review.all
    render json: ReviewSerializer.new(reviews)
  end

  def create
    new_review = Review.new(review_params)
      if new_review.save
        render json: ReviewSerializer.new(new_review)
      else
        render json: new_review.errors
      end
  end
  private 
  def review_params
    params.require(:review).permit(:description)
  end
end
```

##  Building out the frontend

<a href="https://imgur.com/uIfiRhr"><img src="https://i.imgur.com/uIfiRhrh.jpg" title="source: imgur.com" /></a>

We have index.js file with functional programming and Adapters and respective Classes for our models and reviews set like this:

<a href="https://imgur.com/O9fZ6ad"><img src="https://i.imgur.com/O9fZ6adh.jpg" title="source: imgur.com" /></a>

We have EventListener and handleMenuClick function to determine if target is anything besides the menus and I create callback object that has key value pairs and if we matched the targets with the keys in the object we can essentially pull out that function from the object and invoke it: 
```
function handleMenuClick(event){
  if (event.target.id !== menu){
    main.innerHTML = ``
    callbacks[`${event.target.id}`]()
  }
}
```


```
const callbacks = {
  allBooks: renderAllBooks,
  booksReviews: renderAllBooksReviews,
  newBook: renderNewBookForm,
  newReview: renderNewReviewForm
}
```



To learn more check my [Github](https://github.com/ivanadokic/book-reviews) or connect with me on [LinkedIn](https://www.linkedin.com/in/ivana-dokic-b96460120/) or [Twitter](https://twitter.com/LloydPile).


