---
layout: post
title: "The difference between rake db:create and rake db:create:all"
date: 2012-12-10 14:40
comments: true
categories: 
---
`rake db:create`

This command creates the database corresponding to your current environment.

`rake db:create:all` 

This command creates all databases defined in `config/database.yml`. So when you run this command in development for the first time, it will create  production and test databases as well.
