---
layout: post
title: "How To Query NYC Open Datasets with Socrata"
date: 2012-11-14 21:19
comments: true
categories: 
---
NYC provides a ton of data from a variety of sources to the public to use for research and for application development. There's information ranging from Wifi Hotspot Locations to 311 Service requests. You can check out all the datasets here: [https://nycopendata.socrata.com/](https://nycopendata.socrata.com/). As a developer, working with these datasets can be tricky, as the documentation can be unclear and disorganized. Here's a basic primer on how to get started.

###Access the dataset via SODA (Socrata Open Data API)
Most of the datasets have a SODA API endpoint set up that you can hit to get data back. To find the endpoint, open up the dataset, click on the "Export" tab at the top to show the "API" tab. 

{% img /images/endpoint.jpg %}

The endpoint url will look something like this:
```
http://data.cityofnewyork.us/api/views/erm2-nwe9/rows.json
```
Each dataset has a unique identifier which will be important later on, in this instance it's <code>erm2-nwe9</code>.

You can use your browser to hit this url and see what kind of data you get back, however depending on how large the dataset is this could take a very long time, even for a patient person. The json that's returned in this case is unfortunately not very easy to work with, there's hashes of data describing the table/columns in the beginning and then all the actual data in an array at the end of the response.
{% img /images/json_data.jpg %}

I really don't care about anything other the actual data, so how do I get that back? 

###Access the dataset through the right endpoint
It turns out that SODA typically exposes two different endpoints, one under "/api/views" and another under "/resources". The first endpoint is used as a RESTful interface while the other is primarily used to retrieve data. So for the example above these are the two endpoints, and the one we are interested in is the second. If you have the unique id of your dataset, you should be able to substitute it below and begin querying the data you want.
```
http://data.cityofnewyork.us/api/views/erm2-nwe9/rows.json
http://data.cityofnewyork.us/resource/erm2-nwe9.json
```
###Filter the data
No matter what you're trying to do, you probably want to filter the data in some way. You can read the entirety of the query documentation here: http://dev.socrata.com/docs/queries, but the most important one you'll probably be using to start is <code>$limit</code>, which limits the amount of data you get back so the web response will be super fast.
```
http://data.cityofnewyork.us/resource/erm2-nwe9.json?$limit=10
```
Here is a more advanced query that involves filtering by a datetime field. Note that you have to wrap the datetime value in single quotes for this to work.
```
http://data.cityofnewyork.us/resource/erm2-nwe9.json?$limit=10&$where=created_date%3E'2012-11-09'AND created_date > '2012-11-10'
```

At this point, you should be able to get up and running pretty quick. If you have more questions feel free to ask.