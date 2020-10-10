---
layout: post
title: How to Store Spotify Data in 3NF
subtitle: With SQLite3
cover-img: /assets/img/spotify/spotify_thum.jpg
image: /assets/img/spotify/spotify_thum.jpg
tags: [Normalization, SQLite3, Spotify]


---

This post will show how to store Spotify data in the Third Normal Form (3NF) using SQLite. Third Normal Form implies that it's already in 2NF and that there are no transitive relationships between non-prime attributes. In other words, 3NF means that one non-prime attribute cannot be inferred by another non-prime attribute. So, each attribute in the table depends only on the primary key. If you are unfamiliar with normalization, there are many good tutorials. Why not start with [this one](https://www.edureka.co/blog/normalization-in-sql/)?

Why is it important that the data is stored in 3NF? It is common to store data in a relational database in 3NF because it minimizes unnecessary duplication of data, helps to avoid modification anomalies when inserting, deleting, or updating tuples, and simplify queries. 

## Normalization of Spotify data

[Spotify data](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-01-21/readme.md) has 23 columns and it is already in the 1st Normal Form as can be seen from the sample of data below. 

```python
data.shape
```

```python
(32833, 23)
```

```python
data.columns
```

```python
Index(['track_id', 'track_name', 'track_artist', 'track_popularity',
       'track_album_id', 'track_album_name', 'track_album_release_date',
       'playlist_name', 'playlist_id', 'playlist_genre', 'playlist_subgenre',
       'danceability', 'energy', 'key', 'loudness', 'mode', 'speechiness',
       'acousticness', 'instrumentalness', 'liveness', 'valence', 'tempo',
       'duration_ms'],
      dtype='object')
```

|      |               track_id |                                        track_name | track_artist | track_popularity |
| ---: | ---------------------: | ------------------------------------------------: | -----------: | ---------------: |
|    0 | 6f807x0ima9a1j3VPbc7VN | I Don't Care (with Justin Bieber) - Loud Luxur... |   Ed Sheeran |               66 |
|    1 | 0r7CVbZTWZgbTCYdfa2P31 |                   Memories - Dillon Francis Remix |     Maroon 5 |               67 |
|    2 | 1z1Hg7Vb0AhHDiEmnDE79l |                   All the Time - Don Diablo Remix | Zara Larsson |               70 |

As can be seen from the data above, there are a several themes (e.g., tracks, albums, and playlists) and each of them can be saved in a separate table.  For the relational database to be in 3NF, each attribute in the table should depend only on primary key. Obviously, this is not true in the current state of Spotify data. After normalization, I ended up with 9 tables. For more details on how and why these tables were created, please see my code [here](https://github.com/Klalena/BIOS823-Statistical_Programming-for-Big-Data/blob/master/Homework/Spotify_DB_Normalization.ipynb).

Here is a simple ER diagram of the normalized SQLite database for Spotify data:

<img style="float:left; margin-right: 20px;" src="/assets/img/spotify/spotify_er.png" > 



## Fom Pandas DataFrames to SQLite databases 

First, I saved the above noted tables as pandas DataFrames. For example, let's take a look how `album` table was created. 

```python
data = pd.read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-01-21/spotify_songs.csv')

album = data.iloc[:, [4,6]].drop_duplicates()
album.head(3)
```



|      |         track_album_id | track_album_release_date |
| ---: | ---------------------: | -----------------------: |
|    0 | 2oCs0DGTsRO98Gh5ZSl2Cx |               2019-06-14 |
|    1 | 63rPSO264uRjW1X5E6cWv6 |               2019-12-13 |
|    2 | 1HoSmj2eLcsrR0vE9gThr4 |               2019-07-05 |

The next step is to convert pandas DataFrames in SQLite database, which is done with `sqlite3` as follows: 

```python
import sqlite3

#connect to the database
conn = sqlite3.connect('spotify.db')
c = conn.cursor()

#list of tables (DataFrames)
tables = [track, track_name, album, album_name, playlist_name, playlist, track_album, track_playlist, album_playlist]
#names of the tables
tables_names = ['track', 'track_name', 'album', 'album_name', 'playlist_name', 'playlist', 'track_album', 'track_playlist', 'album_playlist']

#convert each table to SQl 
for i, df in enumerate(tables):
    df.to_sql(tables_names[i], con = conn, index = False, if_exists='replace')

```

Now, let's see what tables we have in `spotify.db`.

```python
c.execute(  
"""
SELECT name
FROM sqlite_master
WHERE type = 'table'
""")
#list the names of the tables in the databse
c.fetchall()
```

```python
[('track',),
 ('track_name',),
 ('album',),
 ('album_name',),
 ('playlist_name',),
 ('playlist',),
 ('track_album',),
 ('track_playlist',),
 ('album_playlist',)]
```

All 9 tables are in SQLite database in 3NF! 

And here is how I generated the ER diagram: 

```python
#create ER diagram 
import os 
from eralchemy import render_er

render_er('sqlite:///spotify.db', 'spotify_er.png', mode = 'graph')
```

Now we are ready to run SQL queries! 

## What are the names of playlists that contain instrumentals?

