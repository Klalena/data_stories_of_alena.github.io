---
layout: post
title: Working with the StarWars API in Python
subtitle: Using `requests` package 
cover-img: /assets/img/StarWars_API/yoda_cover.jpg
thumbnail-img: /assets/img/StarWars_API/yoda.jpg
tags: [StarWars API, REST API]

---

As more companies provide access to their data through their APIs, it became increasingly common to use APIs to retrieve data. This tutorial will show how to get data from the [`SWAPI(The Star Wars API)`](https://swapi.dev/documentation) in Python using `requests` package and how to answer the following question: 

**Who is the oldest character in the Star Wars Universe and in which films it was appeared?**

#  Get Data from the Star Wars API 

To retrieve data from SWAPI, we will need to make request to that API. In Python, we will use `requests` package to do so (see below): 

```python
import requests
url = 'http://swapi.dev/api/'
#make request 
response = requests.get(os.path.join(url, 'people/'))
#convert to json format 
data = response.json()
```



Now, let's see how the data looks like for the first person. 

```python
data.keys()
```

`dict_keys(['count', 'next', 'previous', 'results'])`

```python
data['results'][0]
```

```python
{'name': 'Luke Skywalker',
 'height': '172',
 'mass': '77',
 'hair_color': 'blond',
 'skin_color': 'fair',
 'eye_color': 'blue',
 'birth_year': '19BBY',
 'gender': 'male',
 'homeworld': 'http://swapi.dev/api/planets/1/',
 'films': ['http://swapi.dev/api/films/1/',
  'http://swapi.dev/api/films/2/',
  'http://swapi.dev/api/films/3/',
  'http://swapi.dev/api/films/6/'],
 'species': [],
 'vehicles': ['http://swapi.dev/api/vehicles/14/',
  'http://swapi.dev/api/vehicles/30/'],
 'starships': ['http://swapi.dev/api/starships/12/',
  'http://swapi.dev/api/starships/22/'],
 'created': '2014-12-09T13:50:51.644000Z',
 'edited': '2014-12-20T21:17:56.891000Z',
 'url': 'http://swapi.dev/api/people/1/'}
```

However, current `response` only has data for 10 people. To get the data for all people, we will to need loop over urls for  all people (83) like this: 

```python
people = [requests.get('https://swapi.dev/api/people/' + str(i)).json() for i in range(1, 84)]
```

 After getting all the data we need, we will convert it to DataFrame format. To do so, we will use `pd.json_normalize` which normalizes json data into a DataFrame. 

```python
#normalize json 
df = pd.json_normalize(people)
```

# Find the oldest character in the Star Wars Universe

We have several variables for each character;  however, to answer our question, we will just need three columns: `name`, `bith_year`, and `films`. So, we will create a subset inducing only those  three variables. 

```python
subset = df[['name', 'birth_year', 'films']]
subset.head(3)
```

|      |           name | birth_year |                                             films |
| ---: | -------------: | ---------: | ------------------------------------------------: |
|    0 | Luke Skywalker |      19BBY | [http://swapi.dev/api/films/1/, http://swapi.d... |
|    1 |          C-3PO |     112BBY | [http://swapi.dev/api/films/1/, http://swapi.d... |
|    2 |          R2-D2 |      33BBY | [http://swapi.dev/api/films/1/, http://swapi.d... |





We have several variables for each character;  however, to answer our question, we will just need three columns: `name`, `bith_year`, and `films`. So, we will create a subset inducing only those  three variables. 

sample data 

conversion to json format 

Who is the oldest charcter? 

Wondering who is the youngest? 

- include image (if possible)

In which movies Yoda was shot?  