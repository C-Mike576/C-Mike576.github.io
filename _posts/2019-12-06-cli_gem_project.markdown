---
layout: post
title:      "CLI Gem Project"
date:       2019-12-07 03:35:32 +0000
permalink:  cli_gem_project
---


When I started this project I didn't really know where to start, until I started playing D&D with my friends again. 
That got me thinking, What if i could make a program that would let you pick a class and then fight some monsters.

Which led me to dndbeyond.com where I found all the different classes all nicely organized in HTML. After I started it only 
took about 10 hours to reach the point I'm at now. I used Nokogiri to grab the classes, and the monsters. The monster
came from chaoticshiny.com which has a random monster generator that luckily puts them out in a nokogiri readable way.

At first I ran into some trouble getting around dndbeyond's bot protection, I keep on getting 403 errors. I resolved those by adding in a "User-agent" argument when doing the initial scrap. 
```
 Nokogiri::HTML(open(site, "User-Agent" => "Mozilla/5.0 (Windows NT 6.0; rv:12.0) Gecko/20100101 Firefox/12.0 FirePHP/0.7.1"))
```
After those were resolved the rest of the project went quite smoothly. 

# Looking Forward
I would like to add in more features like having your class matter more and giving monsters stats to make it feel more like an old-school text adventure. Giving the monsters stats would be much harder but I look forward to the challenge.

