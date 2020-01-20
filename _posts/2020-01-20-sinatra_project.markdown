---
layout: post
title:      "Sinatra project"
date:       2020-01-20 15:27:36 +0000
permalink:  sinatra_project
---


Contrary to the first project I had a solid plan on what to do for this project. For the sinatra project I decided to do a team builder for one of my favorite tabletop war games, Guild Ball. As I worked through the labs and got into the project proper I realize there is a lot more moving parts that come together to form a basic web app.

# Getting Started 

First I needed to setup the user signup/logout system. Just this part needs quite a few parts before I could continue. Using Activerecord I built a database for my users meanwhile I also setup my database for the teams and the players in said teams.

# Building Forms

With my databases now setup I moved onto making forms. I setup the User systems easy enough. When I got to adding players to teams I encountered one of the limitations of building an app with sinatra. I was unable to populate the form choices with the users previous selections.

# Going Forward

The limitations with building an app with sinatra were quite annoying. I would really like to do is revisit this project with Javascript. Rewriting this app with the ability to update pages without having to reload them would greatly help the usability of the app.

