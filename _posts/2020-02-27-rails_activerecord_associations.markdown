---
layout: post
title:      "Rails ActiveRecord Associations"
date:       2020-02-27 19:19:05 +0000
permalink:  rails_activerecord_associations
---


The relationship between Active Record models is referred to as an association. This relationship adds in many different methods depending on the type of association given to the model. Rails supports six different types of associations, I am going to focus on the three most important to my situation and the methods that they bring.

## belongs_to

This association establishes a one-to-one relationship. For example a song belongs to an artist. That means that a song is assigined to exactly one artist. In your model it would look like:
```
class Song < ApplicationRecord
	belongs_to :artist
end
```
### Methods added with belongs_to

* A getter method (eg. ```@song.artist```)
* A setter method(eg. ```@song.artist = “Shinedown”```)
* build_artist
* create_artist
* create_artist!
* reload_artist

**build_artist**

The ```build_``` method returns a new object of the related type. This method accepts  an argument of the passed attributes and sets the foreign key without saving it to the database.

```
@artist = @song.build_artist(name: “Shinedown”, date_formed: “2001”)
```
Tip: This method is useful for setting up nested forms in your *new* and *create* action of the associated controller (the song controller).

**create_artist**

 Similar to build but attempts to save to the database after passing validations outlined in the model

```
@artist = @song.create_artist(name: “Shinedown”, date_formed: “2001”)
```

**create_artist!**

Does the same as ```create_artist``` but throws an ActiveRecord::RecordInvalid error if it fails validation.

**reload_artist**

This call will load the parent object from the database. This is useful if you already have a previously loaded version and have made unsaved changes and need to revert back to the original version for some reason.

## has_many

This refers to a one-to-many relationship, it is most often found on the opposite side of belongs_to. 
```
class Artist < ApplicationRecord
	has_many :songs
end
```
Remember that belongs_to uses the singular (:artist) and has_many uses the plural (:songs)

### Methods added by has_many

The has_many association adds 16 different methods I’ll focus on just a few I find most useful.

* The getter (eg. ```@artist.songs```)
* .destroy
* .empty?
* .size
* .find
* .where
* .build

**The getter**
```@songs = @artist.songs```
Returns an ```ActiveRecord::Relation``` of related objects, if none are found it returns an empty Relation. 

**.destroy**
```@artist.songs.destroy(@song2)```
Removes one or more objects from the database

**.empty?**
```@artist.songs.empty?```
Returns true if the database doesn’t contain any of the related object.

**.size**
```@artist.songs.size```
Name says it all returns the number of objects in the relation.

**.find**
This method accepts a number or an array and finds then returns object(s).
```
@artist.songs.find(2)	#returns the object with id = 2
@artist.songs.find([3, 5, 9])	#returns the objects with id = (3, 5, 9) in that order
```

**.where**
This method is very powerful as it finds objects in the relation based on the conditions passed in. The objects returned  are “loaded lazily” which means that this method doesn’t query the database. Say your artists makes both long and short songs but you only want the songs that are over 250 seconds then you might have a column in your database table that stores song lengths in seconds you could do something like: 
```@long_songs = @artist.songs.where(song_length > 250)```
The database would only be queried when the objects are accessed with another method.
```@long_song = @long_songs.first```

**.build**
Similar to the ```build_``` method in the belongs_to side of the relation very useful for building nested forms.

**The controller**
```
class SongsController < ApplicationController

	def new
		@artist = Artist.find(params[artist_id])
		@song = @artist.songs.build
	end
	
	def create
	@artist = Artist.find(params[artist_id])
	@song = @artist.songs.build(params.require(:song).permit(:title, :song_length, :artist_id))
	end
```
**The HTML**
*Tip:* Make sure to pass in the nested attribute first when you supply the model after the form_with
```
<%= form_with model: [@artist, @song] do |f| %>
<% if !@artist %> 
        		<%= f.label :artist_id, "Artist” %>
        		<%= f.text_field :artist_id %> 
    	<% end %>
    	<br>
    <%= f.label :title %>
    <%= f.text_field :title %>
    <br>
    <%= f.label :song_length “Length in seconds:” %>
    <%= f.text_area :song_length %>
    <br>
    <%= f.submit %>
<% end %>

```
This form only displays the artist part of the form if it’s accessed from a non-nested route.

# has_many :through
```
class Artist < ApplicationRecord
	has_many :songs
	has_many :genres, through: :songs
end

class Song < ApplicationRecord
	belongs_to :artist
	has_many :genres
end

class Genre < ApplicationRecord
	belongs_to :song
end
```

This relationship functions much like the has_many relation it’s most useful for setting up a “shortcut through” another relationship So you could say an Artist has many songs and  songs have one or more genres, therefore an artist has many genres through songs. After setting up this relation you could say something like: ```@artist.genres```.

# What does it mean?

With all these relationships, plus a few others I didn’t touch on, give us a convenient and easier way of accessing our data in our databases. When I applied  these macros to my program they added in so much functionality that I wasn’t taking advantage of. But after writing this blog and reviewing my code I was able to better utilize the tools I had been given through the powerful Active Record Associations.   

