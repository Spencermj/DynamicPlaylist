# Problem
We want to use [Echonest Playlist] to create an interactive dynamic playlist.

# Question
1. How do you create a dynamic playlist?
2. How do you add interactive elements to a dynamic playlist?
3. What is a taste profile? 

# Resources
1. [Echonest Playlist]

### 1. Creating a dynamic playlist using [Dynamic Playlist]
A dynamic playlist allows much more interactivity and personalization than a static playlist. You can use a few artists, songs, or genres of your choice to create a static playlist that represents your musical preference fairly well, but this playlist will have nowhere near as much versatility and interactivity as a dynamic playlist. Each dynamic playlist created instantiates a new session with a unique session ID, this ID lasts for 24 hours and holds all the information about the playlist. Dynamic playlists keep track of the songs that have already been played as well as any preferences set by the user in real time such as banned/skipped songs and song ratings. By keeping track of previously played songs as well as the user's opinion of certain songs, the playlist can adapt in real time and more accurately match the user's musical preference.

[Playlist Example] shows how to create a basic dynamic playlist based off a few artists. Like with a static playlist, a dynamic playlist is created by entering either a session_catalog or anywhere from one to five artists, songs, or genres. A session_catalog is created from a previous playlist and holds all the feedback from that playback, this allows a user to return to a previous dynamic playlist even after the session ID has expired. The following code creates a dynamic playlist using the artists "yes", "supertramp", and "van halen" as paramaters:

```python
from pyechonest import playlist
dyn_playlist = playlist.Playlist(type='artist', artist=['yes', 'supertramp', 'van halen'])
```

This resource answers the question 1: how do you create a dynamic playlist?


### 2. Adding interactivity with [Feedback]
This method is what sets a dynamic playlist apart from a static playlist, allowing the user to change the preferences of their session in real time. One of the most notable features of [Feedback] is the fact that it allows the user to rate songs and set favorite songs or artists; this allows the session to choose future songs that are similar to songs and artists the user enjoys. Similarly, the user can ban songs or artists and skip songs, making it so that those songs and artists are never played again and similar songs are less likely to be played.

In addition to being able to change the preferences for upcoming songs, the user can the use the [Feedback] method to alter the information that the session has previously recorded. This lets the user set certain songs as "played", meaning they aren't played again during the session, or to set songs as "unplayed" to allow the chosen song to be played again in the future. Finally, the update_catalog paramater can be set to false at any point in time to stop information from being recorded about the session in the session_catalog. Setting the update_catalog paramater to false allows you to make any changes you want to a given session while still being able to reset the session to its original settings.

This resource answers question 2: how do you add interactive elements to a dynamic playlist?


### 3. What is a [Taste Profile]?
Much like a session_catalog, a Taste Profile holds all of a certain user's musical preferences. Unlike a session_catalog, a Taste Profile will never expire. Also unlike a session_catalog, Taste Profiles can only be used to create static playlists. This means that a Taste Profile is essentially how to give a static playlist more individuality, but it still lacks interactivity. A Taste Profile is made up of an item block containing all the basic information about a song as well as a play count, a skip count, a rating, and booleans representing whether the song has been favorited or banned. THe following is the format for a general json item block:

```python
[
 {
 "action":action code. one of ("delete","update","play","skip". Default is "update")
 "item":
    {
         "item_id":any identifier as long as hash(catalog_id+item_id) is unique. [REQUIRED]



         "track_id": rosetta ID OR ENID [OPTIONAL]

         "song_id": rosetta ID OR ENID [OPTIONAL]
         "song_name": song name [OPTIONAL] (song_name, song_id and track_id are mutually exclusive)

         // artist info should not be specified if a song_id or track_id is given
         "artist_id":rosetta ID OR ENID  [OPTIONAL]
         "artist_name":artist name [OPTIONAL] (artist_name and artist_id are mutually exclusive)

         "release":name of release [OPTIONAL]
         "genre":name of genre [OPTIONAL]
         "track_number":integer [OPTIONAL]
         "disc_number":integer [OPTIONAL]
         "url":string of local filename or remote url [OPTIONAL]

         "favorite":bool true/false [OPTIONAL]
         "banned": bool true/false [OPTIONAL]
         "play_count":integer [OPTIONAL]
         "skip_count":integer [OPTIONAL]
         "rating":integer 0..10 [OPTIONAL]


         "item_keyvalues": {
             "class" : ["Primary", "Gold", "Deep Track"],
             "sound" : ["female", "disco", "pop"],
             "mood" :  "upbeat",
             "rating" :  10,
             "tempo" : ["fast", "fast"]      // starts fast, ends fast
         }

     }
  }
 ]
```
You might ask why anyone would use a Taste Profile to create static playlists when dynamic playlists allow all the same functionality, one of the main reasons for this is because you can create a Taste Profile representing your musical tastes before you even create a playlist. The information contained within a session_catalog is created after the user has given input on songs played by during their session, this means that it will only start accurately depicting your musical preferences after you have given your opinion on a great deal of songs. TASTE PROFILE DIRECTORY

This resource answers question 3: what is a taste profile? 

[Echonest Playlist]: http://developer.echonest.com/docs/v4/standard.html
[Dynamic Playlist]: http://developer.echonest.com/docs/v4/standard.html#dynamic
[Playlist Example]: https://github.com/echonest/python-tutorials/blob/master/playlist_api/02_playlist_dynamic_artist.py
[Feedback]: http://developer.echonest.com/docs/v4/standard.html#dynamic-feedback
[Taste Profile]: http://developer.echonest.com/docs/v4/catalog.html
[Taste Profile From Directory]: http://developer.echonest.com/raw_tutorials/faqs/faq_02.html
