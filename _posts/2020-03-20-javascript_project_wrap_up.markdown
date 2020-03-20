---
layout: post
title:      "JavaScript Project Wrap Up"
date:       2020-03-20 19:55:10 +0000
permalink:  javascript_project_wrap_up
---


This project I built a team maker for the Guild ball tabletop game, similar to my sinatra project but more visual and it is a single page app. Now I can finally view the actual cards of the different players, front and back. Ruby is a very different language from Javascript and I learned a lot about it from this project.

# Go Fetch and Class Time

Using an asynchronous language like javascript comes with its own set of interesting challenges. Making sure you're doing selector calls at the right time is important. When doing a `fetch` request you have to remember to put things you want to grab with sector query inside the `then` chain otherwise it will try to execute before the DOM has the item you're looking for. 
In addition to being an asynchronous language javascript is also prototypal meaning that things like classes don’t work like they did in ruby. Javascript uses ES6 syntax to disguise factory functions as classes that look somewhat similar to what I was used to in ruby. Ruby is a language designed for object oriented programming, unlike javascript, so a lot of the repetitive stuff in ruby has been abstracted away over the years. In javascript we are still required to write out all the constructor assignment unlike ruby where its paired down to an `attr_accessor`

# Improvements

I would like to add more teams to choose from to improve this project. As it sits right now I would only need to add the players to the backend database and the app should automatically add them right into the front end view. I would also like to be able to view the different teams individually as the app is right now it would just display all the players in one big lump. Being able to sort between Fishermen and Brewers for instance would be nice and something I plan on adding later. I’m looking forward to getting to know React and Redux as I continue further in the program.

