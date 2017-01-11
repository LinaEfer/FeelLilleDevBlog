---
layout: post
title:  Firebase Authentification
date:   2016-12-12 12:55:20
author: Vasilina
categories: Technical
tags:	Authentification Firebase
---

We continue to work with Firebase. In this post, we will test the authentication service. User authentication is required in most applications. This allows you to share access, securely store user’s personals data in the cloud and provide a personalized experience to all user devices.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

In our project we need it because we have the intention to allow people to connect to our app from different ways. The simplest would be registered using mail address and password. But we also would like them to be able to connect with others services such as facebook, google.. etc
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

Firebase provides easy-to-use backend and ready-made user interface library to implement user authentication in your application. It supports authentication and via email and a password, and by means of the identification of such popular providers like Google, Facebook, Twitter and GitHub.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

To start with Firebase you can do a short tutorial proposed by [Firebase Web Codelab](https://codelabs.developers.google.com/codelabs/firebase-web/#0). This short course will tell you every basis of Firebase, and especially how to create and configure your first project.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

You can manage your project by going to the Firebase console. In order to control the input settings, select in the menu left side item "Authentication".
On the "SIGN IN", you can choose different ways to authenticate. We will look first the authentication option using the email address and password. For this in  Auth section > SIGN IN METHOD tab you need to enable the  Email/password Sign-in Provider and click SAVE.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

Add email username and password, which will be involved in the authentication process.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

<img src="../../../../assets/posts/FirebaseAuth.png">


Now we are ready to work with Firebase. Create a new account by passing the new user's email address and password to ```createUserWithEmailAndPassword``` :
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
FriendlyChat.prototype.signInLogin = function(){
    var email = document.getElementById("email").value;
    var password = document.getElementById("password").value;
    firebase.auth().signInWithEmailAndPassword(email,password).catch(function(error) {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  console.log(errorMessage);
}); };
```

Save the changes and restart the server. Now you can try to log in using the ID and password which you created. If authentication failed, the console must prompt this message : "The password is invalid or the user does not have a password."
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

In the same way, you can implement a user registration with other services. The main difference will be just in instance of the provider object. 
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

**Example for Google Sign-in:**
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
FriendlyChat.prototype.signIn = function() {
  // Sign in Firebase using popup auth and Google as the identity provider.
  var provider = new firebase.auth.GoogleAuthProvider();
  this.auth.signInWithPopup(provider);
};
```

**Example for Facebook Sign-in:**
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
FriendlyChat.prototype.signIn = function() {
  // Sign in Firebase using popup auth and Facebook as the identity provider.
  var provider = new firebase.auth.FacebookAuthProvider();
  this.auth.signInWithPopup(provider);
};
```

**Example for Twitter Sign-in:**
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
FriendlyChat.prototype.signIn = function() {
  // Sign in Firebase using popup auth and Twitter as the identity provider.
 var provider = new firebase.auth.TwitterAuthProvider();
  this.auth.signInWithPopup(provider);
};
```

Example for GitHub Sign-in:
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}

```javascript
FriendlyChat.prototype.signIn = function() {
  // Sign in Firebase using popup auth and Github as the identity provider.
 var provider = new firebase.auth.GithubAuthProvider();
  this.auth.signInWithPopup(provider);
};
```

In this post, we briefly looked the possibilities of using the authentication by Firebase. For more information you can get acquainted with the material provided [Firebase documentation](https://firebase.google.com/docs/auth/web/manage-users) Manage Users in Firebase.
{: style="text-align: justify; font-family: Verdana, Geneva, sans-serif"}