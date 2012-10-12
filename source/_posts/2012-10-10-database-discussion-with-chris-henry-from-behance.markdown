---
layout: post
title: "Database Discussion with Chris Henry from Behance"
date: 2012-10-10 22:06
comments: true
categories: 
---
Chris Henry, the CTO of [Behance](http://behance.net) came in to the Flatiron School today to give us a primer on databases and MySQL. He showed us a few cool things that I didn't know about before, and also gave us some insight on how a real-world application with many users is architected and scaled. There was lots of advanced shit but here are some things I took away:

##Slow Log
MySQL writes to a "slow log" any queries that take longer than a given threshold (Behance uses 1 sec) to execute. This is great tool to use to debug the reason why it takes your page 20 seconds to load and no one is using your site. Use "EXPLAIN EXTENDED" to get into the guts of what a query is actually doing.

##Index Everything
Don't index everything, but apparently adding indexes will solve 99% of the problems that you run into.

##Denormalization
Whenever I read documentation on denormalization, I think to myself: "Ok, I get the concept, but when will I ever need to do this?". Behance does something really interesting. For aggregate data that requires multiple joins or are really inefficient, they denormalize that data and store it with their "main" objects. To support that, they have additional database clusters that store the actual data that is being aggregated. If I understood that correctly, it means they store "Tag" rows elsewhere (MongoDB?) but denormalize "Tag" counts and add them to one of their main models. 
