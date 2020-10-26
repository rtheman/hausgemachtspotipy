
# hausgemachtSpotiPy

**hausgemachtspotipy** is a Python package that access music artists, albums, and tracks, directly from the Spotify Data Catalogue via Spotify Web API endpoints .

Inspired by the [SpotiPy](https://pypi.org/project/spotipy/) Python package, the **hausgemachtspotipy** package focuses on easily querying music artists, albums, and tracks from Spotify.


## Table of Contents
1. [Installation](#installation)
1. [Quick Start](#quick-start)
1. [Functions](#functions)

---
---

## Installation

```python
pip install hausgemachtspotipy
```

To upgrade
```python
pip install hausgemachtspotipy --upgrade
```



## Quick Start

**Import Libraries**
```
import hausgemachtspotipy as hausSP
```

**Define credentials**
```
client_id = "cd1845f23d914228b14f6bed139ee594"
client_secret = <insert secret key>
```
Details on obtaining Spotify API credentials, head to https://developer.spotify.com/dashboard/

**Create Spotify API token**
```
sp = hausSP.SpotifyAPI(client_id, client_secret)
```
**Find Artist's details**
```
artists = sp.search(query="Justin Timberlake")
print(artists)
```



## Functions
Full list of functions of this library includes:

1. **Search**.  This
below codebase shows...
```python
artists = sp.search(query="Chainsmokers")

# Convert json to dataframe
df_artists = pd.json_normalize(artists)

df_artists['artists.items'][0][0]['id']
# Returns, '69GGBxA162lTqCwzJG5jLp'
```

2. **get_artist**.  Get Spotify catalog information for a single artist identified by their unique Spotify ID.
For syntax and input parameters, refer to Spotify's API endpoint reference [here](https://developer.spotify.com/documentation/web-api/reference/artists/get-artist/).

```python
artist_resp = sp.get_artist("69GGBxA162lTqCwzJG5jLp")
```

3. **get_artist_albums**.  List artist's albums, `The Chainsmokers`, via Spotify Artist's ID, `69GGBxA162lTqCwzJG5jLp`
below codebase shows...
```python
albums = sp.get_artist_albums("69GGBxA162lTqCwzJG5jLp")
df_albums = pd.json_normalize(albums)

albums_count = df_albums['total']
print(Albums_count)
# RETURNS:
# 271

album_id = df_albums['items'][0][3]['id']
album_total_tracks = df_albums['items'][0][3]['total_tracks']
album_name = df_albums['items'][0][3]['name']
album_release_date = df_albums['items'][0][3]['release_date']
print(f"Album ID:{album_id}, Number of Tracks:{album_total_tracks}, Album Name:{album_name}, Release Date:{album_release_date}")
# RETURNS:
# Album ID:6ZvDJs17O3woQirttKRYCG, Number of Tracks:10, Album Name:Sick Boy, Release Date:2018-12-14
```

4. **get_album** gets Spotify catalog information for a single album.
For syntax and input parameters, refer to Spotify's API endpoint reference [here](https://developer.spotify.com/documentation/web-api/reference/albums/get-album/).
```python
album = sp.get_album("6ZvDJs17O3woQirttKRYCG")
df_album = pd.json_normalize(album)
print(df_album)
```

5. **get_album_tracks** gets Spotify catalog information about an album’s tracks. Optional parameters can be used to limit the number of tracks returned.
For syntax and input parameters, refer to Spotify's API endpoint reference [here](https://developer.spotify.com/documentation/web-api/reference/albums/get-albums-tracks/).
```python
tracks = sp.get_album_tracks('6ZvDJs17O3woQirttKRYCG')

df_tracks = pd.json_normalize(tracks)

track_id = df_tracks['items'][0][0]['id']
track_num = df_tracks['items'][0][0]['track_number']
track_name = df_tracks['items'][0][0]['name']
track_duration = df_tracks['items'][0][0]['duration_ms']
track_preview_url = df_tracks['items'][0][0]['preview_url']
print(f"Track ID: {track_id}, Track Num: {track_num}, Name: {track_name}, Duration: {track_duration}, Preview URL: {track_preview_url}")
```

6. **get_track**.  This
below codebase shows...
```python
blah
```

7. **get_track_features**.  This
below codebase shows...
```python
blah
```
