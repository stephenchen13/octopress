---
layout: post
title: "Hello World!"
date: 2012-10-03 15:16
comments: true
categories: 
---
Deploying Octopress for the first time turned out to be fairly easy. I took a slightly different approach than the standard installation documentation, I wanted to store the codebase in my Github repository as well as deploy to Heroku. To do this some slight customization is needed:
<ol><li>Edit .git/config and rename the current 'origin' remote to something else (upstream).</li><li>Add a remote for your github repository <code>git remote add origin git@github.com:stephenchen13/octopress.git</code></li><li>Add a remote for your heroku repository <code>git remote add heroku git@heroku.com:frozen-citadel-3574.git</code></li><li>Regenerate everything necessary, and now you can push to both Github and Heroku</li></ol>
Blog away!