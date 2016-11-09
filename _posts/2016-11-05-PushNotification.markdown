---
layout: post
title:  "Push Notification - Alert People of Event"
date:   2016-11-05 22:55:20
author: JF
categories: Technical
tags:	Push Notification Firebase Ionic Javascript

---

## Push Notification

Hello,
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif;"}
Today we need to talk about push notification because it is something we need to prevent people that the event they subscribe is starting soon !
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif;"}

It is the first technical post I'm writing and not the easiest one because the system I'll explain is not the easiest one.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

To send push notifications using no didicated server I used two different system linked to the app :
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}
* We decided to use [Firebase](https://firebase.google.com/) as back-end. And Firebase has a system call FCM (Firebase Cloud Messaging) that allow us to send notification from an online console.
* We also use [IonicCloud](https://ionic.io/cloud) that allow us to push from an ionic app a json file that contains a device ID, a notification message and a schedule
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

---

## How it works ?

I made a little scheme to explain that because I think it is easier to understand.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

<img src="../../../../assets/posts/schemaPushNotif.png" title="Push Notification Scheme">

We have three entities : FeelLille application, IonicCloud and Firebase. The idea is to send a json file containing an event with a date and a device ID (to tell ionic it's this device that will receive the notification). The json file is sent by FeelLille application.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}
Ionic will transform it into a request. When the date has come Ionic send the request to Firebase.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}
Finally Firebase process the request and send the notification back to the Device.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

---

## Development part

* First things to do is to set up the phonegap plugin using the command :
```cordova plugin add phonegap-plugin-push --variable SENDER_ID=12341234 --save```
The SENDER_ID is the ID provided by Firebase API.

Then you need to add the module ```[ionic.cloud]``` to your application.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

* Second things to do is to register the Device ID by the app. Please see the little piece of code forward.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
$ionicPush.register().then(function(t) {
  return $ionicPush.saveToken(t);
}).then(function(t) {
  console.log('Token saved:', t.token);
});
```

* Third things to do is to prepare the json file with the right element to send to ionic cloud.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
function config($stateProvider, $urlRouterProvider,$ionicCloudProvider) {
  $ionicCloudProvider
  .init({
    "core" : {
      "app_id" :"Your Ionic Cloud app ID"
    },
    "push": {
      "sender_id": "Firebase SENDER ID",
      "pluginConfig": {
        "ios": {
          "badge": true,
          "sound": true
        },
        "android": {
          "iconColor": "#343434"
        }
      }
    }
  });
```

* Four things to do is to tell your app to monitor if a notification is arriving. I put this in the main controller.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
$scope.$on('cloud:push:notification', function(event, data) {
  var msg = data.message;
  alert(msg.title + ': ' + msg.text);
});
```

Once there you will be able to receive notification from Firebase. On a next post we will see how to send a schedule notification.