---
layout: post
title:  Back-End Scheme
date:   2017-01-11 12:55:20
author: JF
categories: Technical
tags:	Back-End xpath json node
---

On the previous post, I talked about generals things in back-end services. But I have in mind that explains a such things need a scheme to be more understandable. So I have realized a technical scheme on how the actions are processed.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

<img src="../../../../assets/posts/BackEnd.png">



We can find back our three process :
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

* xpath extract info from sources and put it into a json file (datas.json) after deleted duplicates and empty/incomplete results. 
* evaluate takes to input to sort what to update in database and returns an array written in a jsonfile (datas2.json). Inputs are :
   * a database (firebase) query returning values from the base.
   * datas.json returning the previous results.
* update will just add or update value on the db put in datas2.json
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}