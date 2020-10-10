---
layout: post
title: How to Store Spotify Data in 3NF
subtitle: With SQLite3
cover-img: /assets/img/spotify/spotify_thum.jpg
image: /assets/img/spotify/spotify_thum.jpg
full-width: true
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

| track_id |             track_name |                                      track_artist | track_popularity | track_album_id |       track_album_name |                          track_album_release_date | playlist_name | playlist_id |         playlist_genre |  ... |  key | loudness |   mode | speechiness | acousticness | instrumentalness | liveness | valence | tempo | duration_ms |        |
| -------: | ---------------------: | ------------------------------------------------: | ---------------: | -------------: | ---------------------: | ------------------------------------------------: | ------------: | ----------: | ---------------------: | ---: | ---: | -------: | -----: | ----------: | -----------: | ---------------: | -------: | ------: | ----: | ----------: | ------ |
|        0 | 6f807x0ima9a1j3VPbc7VN | I Don't Care (with Justin Bieber) - Loud Luxur... |       Ed Sheeran |             66 | 2oCs0DGTsRO98Gh5ZSl2Cx | I Don't Care (with Justin Bieber) [Loud Luxury... |    2019-06-14 |   Pop Remix | 37i9dQZF1DXcZDD7cfEKhW |  pop |  ... |        6 | -2.634 |           1 |       0.0583 |           0.1020 | 0.000000 |  0.0653 | 0.518 |     122.036 | 194754 |
|        1 | 0r7CVbZTWZgbTCYdfa2P31 |                   Memories - Dillon Francis Remix |         Maroon 5 |             67 | 63rPSO264uRjW1X5E6cWv6 |                   Memories (Dillon Francis Remix) |    2019-12-13 |   Pop Remix | 37i9dQZF1DXcZDD7cfEKhW |  pop |  ... |       11 | -4.969 |           1 |       0.0373 |           0.0724 | 0.004210 |  0.3570 | 0.693 |      99.972 | 162600 |
|        2 | 1z1Hg7Vb0AhHDiEmnDE79l |                   All the Time - Don Diablo Remix |     Zara Larsson |             70 | 1HoSmj2eLcsrR0vE9gThr4 |                   All the Time (Don Diablo Remix) |    2019-07-05 |   Pop Remix | 37i9dQZF1DXcZDD7cfEKhW |  pop |  ... |        1 | -3.432 |           0 |       0.0742 |           0.0794 | 0.000023 |  0.1100 | 0.613 |     124.008 | 176616 |

3 rows × 23 columns

