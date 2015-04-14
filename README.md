# Problem
We want to use [Echonest Playlist] to create an interactive dynamic playlist.

# Question
1. How do you create a dynamic playlist?
2. How do you add interactive elements to a dynamic playlist?
3. What is a taste profile? 

# Resources
1. [Echonest Playlist]

### 1. Creating a dynamic playlist using [Dynamic Playlist]
A dynamic playlist allows much more interactivity and personalization than a static playlist. You can use a few artists, songs, or genres of your choice to create a static playlist that represents your musical preference fairly well, but this playlist will have nowhere near as much versatility as a dynamic playlist. Each dynamic playlist created instantiates a new session with a unique session ID, this ID lasts for 24 hours and holds all the information about the playlist. Dynamic playlists keep track of the songs that have already been played as well as any preferences set by the user in real time such as banned/skipped songs and song ratings.

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


This resource answers question 3: what is a taste profile? 

[Echonest Playlist]: http://developer.echonest.com/docs/v4/standard.html
[Dynamic Playlist]: http://developer.echonest.com/docs/v4/standard.html#dynamic
[Playlist Example]: https://github.com/echonest/python-tutorials/blob/master/playlist_api/02_playlist_dynamic_artist.py
[Feedback]: http://developer.echonest.com/docs/v4/standard.html#dynamic-feedback
