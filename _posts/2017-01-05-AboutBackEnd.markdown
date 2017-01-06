---
layout: post
title:  About Back-End
date:   2017-01-05 12:55:20
author: JF
categories: FeelLille
tags:	Back-End xpath json node heroku
---

Since the beginning of the winter holiday I'm working on the back-end part of the project. The goal of this back-end is to collect event-data from websites and format it to put it back to firebase (our database).

For this we have the intention to work with nodeJS and we have subscribed to Heroku to host this. It is possible to host on Heroku for free but it is limited to 1 millions of request by months.

This is organized as following :
* First, we need to retrieve data for this we use two node module : xmldom and xpath to do xpath request on HTML as we can do on XML document.
* Second, when we have retrieved the data we need to organize them in a JSON file. By organize, I mean delete duplicate, delete empty and format it in a good JSON array.
* Third, in order to push it in firebase we first need to compare with the actual data we have in base to check if it isn't already added.

Once everything there has been done it is needed to use a scheduler to schedule right the data. By chance there's a node module called 'cron' that allow this. With cron you can tell a script to run each X times. We choose to run it each days.
This choice is because we think that we can add enough events in one day to maintains good content and to not exceed the limit of heroku's request for free account.

In next post talking about back-end I have the intention to talk a bit deeper about some of the point listed in organization part.