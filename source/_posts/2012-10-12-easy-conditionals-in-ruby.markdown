---
layout: post
title: "Conditionals and Null References in Ruby"
date: 2012-10-12 13:44
comments: true
categories: 
---
One of the most common errors that haunt all programmers in almost all languages is the Null Reference Exception. Objects get initialized all the time from all kinds of different sources, and a lot of times those objects come back "null" or "nil" in Ruby. Because of this, programmers spend a lot of time protecting their code from breaking. It's a common pattern to check if your object is "null" or "nil" before calling one of it's methods. There's a couple ways this can be done in Ruby that read a lot nicer than other languages, and take less plumbing code to accomplish.

##the classic "if" statement
``` ruby ruby version
obj.name if obj
```
``` c# c# version
if (obj != null) obj.name
```

##the ternary operator
``` ruby ruby version
a = obj ? obj.name : ""
```
``` c# c# version
string a = obj != null ? obj.name : "";
```
The ternary operator allows you to specify a default statement to execute in case your conditional evaluates to false. In Ruby, this line of code is 7+ characters shorter, which is why lazy programmers love Ruby.

##unless
"unless" almost exactly like an "if" statement, but is often used instead of "if !" because it is more readable
``` ruby
a = obj unless my_array.include?(obj)
a = obj if !my_array.include?(obj)
```

##tl;dr
Get real familiar with the "if", ternary, and "unless" operators and protect yourself from null references. What other ways do you use to protect your code?
