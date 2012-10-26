---
layout: post
title: "Easy datetime comparison with ActiveRecord and Rails"
date: 2012-10-25 21:26
comments: true
categories: 
---

Using ActiveRecord is great because of all the built in functionality, but combine ActiveRecord with all the headaches that come with dates and datetime and it can get pretty intimidating. In most web applications that you build you'll probably find yourself needing to filter a set of ActiveRecord objects by date, whether it is a date_created field or something else. These are a few things that made this extremely easy for me to understand. I'm not going to cover formatting datetime display because that is another post for another day. 

## Check the table
First of all, you want to inspect your database table schema and determine what type of field you are comparing against. Your ActiveRecord model can have either 'date' or 'datetime' data types so you'll want to make sure you use the corresponding 'Date' or 'DateTime' Ruby classes. You can actually compare 'Date' and 'DateTime' objects against one another:
```ruby
DateTime.now > Date.today
=> true
```
However if you don't realize that you are comparing two different types of data you may get unexpected results in your application.

## Use built in ActiveSupport methods
"Active Support is a collection of various utility classes and standard library extensions that were found useful for Rails. All these additions have hence been collected in this bundle as way to gather all that sugar that makes Ruby sweeter." -http://as.rubyonrails.org/
<!-- For more on syntactic sugar check out this great blog post
link to Akiva -->

This is the documentation for the ActiveSupport DateTime methods:
[http://as.rubyonrails.org/classes/ActiveSupport/CoreExtensions/DateTime/Calculations.html](http://as.rubyonrails.org/classes/ActiveSupport/CoreExtensions/DateTime/Calculations.html)

And this is the documentation for the ActiveSupport Date methods:
[http://as.rubyonrails.org/classes/ActiveSupport/CoreExtensions/Numeric/Time.html](http://as.rubyonrails.org/classes/ActiveSupport/CoreExtensions/Numeric/Time.html)

With ActiveSupport you can easily query your database with ActiveRecord like this:

``` ruby
  def self.recent_images
    Image.where("created_at > ?", 7.day.ago)
  end

  def self.this_months_images
    Image.where("created_at > ?", DateTime.now.beginning_of_month)
  end

  def self.expired?
    expiration_date > created_at.advance(:months => 2, :days => 10)
  end 
```
  
TLDR:
Instead of creating or hardcoding your own DateTime and Date objects, use built in ActiveSupport methods in your ActiveRecord queries.