---
layout: post
title:  Data Modeling
date:   2016-12-20 12:55:20
author: JF
categories: FeelLille
tags:	Data Model Structure
---

We recently approved the structure of data modeling with the coach. Speaking about structuring data could reveal a little bit more about features.

See the model below :

<img src="../../../../assets/posts/DataModel.png">

> It is important to note that working with firebase as database implies working with a NoSQL DB.

## DataModel Structure

In this section I will describe the role of each table that would be called document in NoSQL.

* User : contains the data of user, I just put usrename in the scheme. But it will contains more things such like description, profile picture... etc
* Event : contains the data of event. I'm deeply attached to link data of event to a place for some reason I will explain later.
* Place : contains the data for a place which is linked to an Event.
* Category : contains the data of category for an Event.
* EventUser & PlaceUser : contains the data which allow user to interact with them.

## Details about Event & Place

Arrived at this point of the article, It is important to give an explaination about the choice to separate Event and Place.
Seperate Event and Place would allow :

* people to like Event and Place seperatly. In this case it would be easier for users to find more event on this place.
* to improve the performance of the recommender system. Indeed, we intend to deploy a powerful system of recommendation. For this we need to divide the data as strictly as we can.

## Details about EventUser & PlaceUser

I talked about interaction between the user and the group Place+Event.

Allowing people to interact with Events and Places will improve the recommendation and their ability to find events more quickly and more easily. We have the intention to implements a like-system.And also to give the possibility to see who is participating to Events. 