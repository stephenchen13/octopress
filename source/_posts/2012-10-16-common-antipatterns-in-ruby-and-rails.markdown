---
layout: post
title: "Common Antipatterns in Ruby"
date: 2012-10-16 17:12
comments: true
categories: 
---
##What is an antipattern?
An antipattern is generally a common solution to a problem that is ineffective, or has negative consequences. It can result from not knowing how to solve a particular problem, not caring how it's solved, or using a correct pattern in a wrong context. Tom Crinson has a great presentation on antipatterns on speakerdeck that can be found [here](https://speakerdeck.com/u/mrjaba/p/ruby-rails-antipatterns). Here are a few examples of antipatterns that I found interesting:

##If True Else False
If the block of code that is executed as a result of your conditional is simply a boolean value, forget about writing out the entire if/else statement. Just return the evaluated result of the conditional. So instead of this:
```ruby
def horrible_if_else
	if @jason_kidd.is_old? && @jason_kidd.is_drunk?
		return true
	else
		return false
end
```
You can do this instead:
```ruby
def better_if_else
	@jason_kidd.is_old? && @jason_kidd.is_drunk?
end
```

##Violating Demeter: Aka Train Wreck Code
These rules make up Demeter's Law:
+You can play on your own.
+You can play with your own toys (but you can't take them apart)
+You can play with toys that were given to you.
+You can play with toys you've made yourself.

Other than sounding kind of creepy, the main side effect of this law is that you shouldn't chain call methods that belong to a different class than you're original object.

The following code violates this principle:
```ruby
	if knicks.players.first.age.older_than?(40)
		"wow they are old"
	end
```
Instead, you should refactor the code so it looks more like this:
```ruby
	if knicks.ages_older_than?(40)
		"wow they are old"
	end
```

One of the first things I learned about Ruby is that it is an opinionated language. Therefore there are tons of antipatterns that exist in Ruby because there is a right way to do things, and there is a wrong way to do things. Leave a comment if you've run into any interesting antipatterns while coding. 
