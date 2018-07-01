# The Industrial Subset of the Million Playlist Dataset
The Industrial Subset of the Million Playlist Dataset contains 1,000
playlists of the Million Playlist Dataset.  It can be used by researchers interested
in exploring how to improve the music listening experience.

## What's in the Industrial Subset of the Million Playlist Dataset
The ISMPD contains 1,000 playlists from the Million Playlist Dataset These playlists
were created during the period of January 2010 through October 2017.
Each playlist in the ISMPD contains a playlist title, the track list
(including track metadata) editing information (last edit time, 
number of playlist edits) and other miscellaneous information 
about the playlist. See the **Detailed
Description** section for more details.


## License
Usage of the Industrial Subset of the Million Playlist Dataset is subject to these 
[license terms](https://recsys-challenge.spotify.com/license)

## Citing the Industrial Subset of the Million Playlist Dataset

Citation information for the dataset can be found at
[recsys-challenge.spotify.com/dataset](https://recsys-challenge.spotify.com/dataset)


## Getting the dataset
The dataset is available at [recsys-challenge.spotify.com/dataset](https://recsys-challenge.spotify.com/dataset)

## Verifying your dataset
You can validate the dataset by checking the md5 hashes of the data.  From the top level directory of the ISMPD:
   
    % md5sum -c md5sums
  
This should print out OK for each of the slice files in the dataset.

You can also compute a number of statistics for the dataset as follows:

    % cd <ismpd directory>
    % python src/stats.py .
  
The output of this program should match what is in 'stats.txt'. 

## Detailed description
The Industrial Subset of the Million Playlist Dataset consists of one json file called ismpd.json. 

This file is a JSON dictionary with two fields:
*info* and *playlists*.

### `info` Field
The info field is a dictionary that contains general information about the particular slice:

   * ***version*** -  - the current version of the ISMPD (which should be v1)
   * ***description*** - a description of the ISMPD
   * ***license*** - licensing info for the ISMPD
   * ***generated_on*** - a timestamp indicating when the slice was generated.

### `playlists` field 
This is an array that typically contains 1,000 playlists. Each playlist is a dictionary that contains the following fields:


* ***pid*** - integer - playlist id - the MPD ID of this playlist. This is an integer between 0 and 999,999.
* ***name*** - string - the name of the playlist 
* ***description*** - optional string - if present, the description given to the playlist.  Note that user-provided playlist descrptions are a relatively new feature of Spotify, so most playlists do not have descriptions.
* ***modified_at*** - seconds - timestamp (in seconds since the epoch) when this playlist was last updated. Times are rounded to midnight GMT of the date when the playlist was last updated.
* ***num_artists*** - the total number of unique artists for the tracks in the playlist.
* ***num_albums*** - the number of unique albums for the tracks in the playlist
* ***num_tracks*** - the number of tracks in the playlist
* ***num_followers*** - the number of followers this playlist had at the time the ISMPD was created. (Note that the follower count does not including the playlist creator)
* ***num_edits*** - the number of separate editing sessions. Tracks added in a two hour window are considered to be added in a single editing session.
* ***duration_ms*** - the total duration of all the tracks in the playlist (in milliseconds)
* ***collaborative*** -  boolean - if true, the playlist is a collaborative playlist. Multiple users may contribute tracks to a collaborative playlist.
* ***tracks*** - an array of information about each track in the playlist. Each element in the array is a dictionary with the following fields:
   * ***track_name*** - the name of the track
   * ***track_uri*** - the Spotify URI of the track
   * ***album_name*** - the name of the track's album
   * ***album_uri*** - the Spotify URI of the album
   * ***artist_name*** - the name of the track's primary artist
   * ***artist_uri*** - the Spotify URI of track's primary artist
   * ***duration_ms*** - the duration of the track in milliseconds
   * ***pos*** - the position of the track in the playlist (zero-based)

Here's an example of a typical playlist entry:
  
        {
            "name": "musical",
            "collaborative": "false",
            "pid": 5,
            "modified_at": 1493424000,
            "num_albums": 7,
            "num_tracks": 12,
            "num_followers": 1,
            "num_edits": 2,
            "duration_ms": 2657366,
            "num_artists": 6,
            "tracks": [
                {
                    "pos": 0,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:7vqa3sDmtEaVJ2gcvxtRID",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Finalement",
                    "album_uri": "spotify:album:2KrRMJ9z7Xjoz1Az4O6UML",
                    "duration_ms": 166264,
                    "album_name": "Dancing Chords and Fireflies"
                },
                {
                    "pos": 1,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:23EOmJivOZ88WJPUbIPjh6",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Betty",
                    "album_uri": "spotify:album:3lUSlvjUoHNA8IkNTqURqd",
                    "duration_ms": 235534,
                    "album_name": "Endless Smile"
                },
                {
                    "pos": 2,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:1vaffTCJxkyqeJY7zF9a55",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Some Beat in My Head",
                    "album_uri": "spotify:album:2KrRMJ9z7Xjoz1Az4O6UML",
                    "duration_ms": 268050,
                    "album_name": "Dancing Chords and Fireflies"
                },
                // 8 tracks omitted
                {
                    "pos": 11,
                    "artist_name": "Mo' Horizons",
                    "track_uri": "spotify:track:7iwx00eBzeSSSy6xfESyWN",
                    "artist_uri": "spotify:artist:3tuX54dqgS8LsGUvNzgrpP",
                    "track_name": "Fever 99\u00b0",
                    "album_uri": "spotify:album:2Fg1t2tyOSGWkVYHlFfXVf",
                    "duration_ms": 364320,
                    "album_name": "Come Touch The Sun"
                }
            ],

        }


## Tools
There are some tools that you can use with the dataset.
### stats.py
This python program will iterate through the entire ISMPD and display summary information about the contents of the MPD.

Usage:

    % python src/stats.py data
    

## How was the dataset built
The Million Playist Dataset is created by sampling playlists from the billions of playlists that Spotify users have created over the years.  Playlists that meet the following criteria are selected at random:

 * Created by a user that resides in the United States and is at least 13 years old
 * Was a public playlist at the time the ISMPD was generated
 * Contains at least 5 tracks
 * Contains no more than 250 tracks
 * Contains at least 3 unique artists
 * Contains at least 2 unique albums
 * Has no local tracks (local tracks are non-Spotify tracks that a user has on their local device)
 * Has at least one follower (not including the creator)
 * Was created after January 1, 2010 and before December 1, 2017
 * Does not have an offensive title
 * Does not have an adult-oriented title if the playlist was created by a user under 18 years of age

Additionally, some playlists have been modified as follows:

 * Potentially offensive playlist descriptions are removed
 * Tracks added on or after November 1, 2017 are removed

Playlists are sampled randomly, for the most part, but with some dithering to disguise the true distribution of playlists within Spotify. [Paper tracks](https://en.wikipedia.org/wiki/Fictitious_entry) may be added to some playlists to help us identify improper/unlicensed use of the dataset.

The industrial Subset of the Million Playlist Dataset consists of the a thousand playlists sampled from  the Million Playlist Dataset.
