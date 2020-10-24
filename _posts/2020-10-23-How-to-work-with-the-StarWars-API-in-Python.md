---
layout: post
title: Working with the StarWars API in Python
subtitle: Using requests  package 
cover-img: /assets/img/StarWars_API/yoda_cover.jpg
thumbnail-img: /assets/img/StarWars_API/yoda.jpg
tags: [StarWars API, REST API]

---

As more companies provide access to their data through their APIs, it became increasingly common to use APIs to retrieve data. This tutorial will show how to get data from the [`SWAPI(The Star Wars API)`](https://swapi.dev/documentation) in Python using the `requests` package and how to answer the following question: 

**Who is the oldest character in the Star Wars Universe and in which films it was appeared?**

#  Get Data from the Star Wars API 

To retrieve data from SWAPI, we will need to make a request to that API. In Python, we will use the `requests` package to do so (see below): 

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

However, the current `response` only has data for 10 people. To get the data for all people, we will need to loop over URLs for all people (83) like this:  

```python
people = [requests.get('https://swapi.dev/api/people/' + str(i)).json() for i in range(1, 84)]
```

 After getting all the data we need, we will convert it to the DataFrame format. To do so, we will use `pd.json_normalize` which normalizes JSON data into a DataFrame. 

```python
#normalize json 
df = pd.json_normalize(people)
```



### Data Cleaning

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

Next, we will clean our data by removing observations with missing values ([#16](https://swapi.dev/api/people/17/) ) and with `unknown` `birth_year` as follows: 

```python
#remove observations with 'unknown' years 
subset = subset[subset.birth_year != 'unknown']
#remove a record with missing data 
subset = subset.drop(16).reset_index(drop = True)
subset.shape
```

```python
(43, 3)
```



# Find the oldest character in the Star Wars Universe

According to the [documentation](https://swapi.dev/documentation), `birth_year` is 'the birth year of the person, using the in-universe standard of BBY or ABY - Before the Battle of Yavin or After the Battle of Yavin. The Battle of Yavin is a battle that occurs at the end of Star Wars episode IV: A New Hope.'

Let's check if we have characters from both periods. 

```python
subset.birth_year.str.contains('BBY').sum()
43
```

It seems that all characters were born Before the Battle of Yavin (BBY). 

Next, we will need to extract `year` from `birth_year` column. We can do so using `regex` as shown below. 

```python
#Extract year from birth_year column and save it as DataFrame 'year'. 
year = pd.DataFrame(subset.birth_year.str.extractall(r'(\d+.\d+|\d+)').astype(float)) 
year = year.droplevel(1)
year.columns = ['year']
```

And concatenate both data frames `Year ` with `Subset`

```python
subset = pd.concat((subset,year), axis = 1)

subset.head()
```

|      |           name | birth_year |                                             films |  year |
| ---: | -------------: | ---------: | ------------------------------------------------: | ----: |
|    0 | Luke Skywalker |      19BBY | [http://swapi.dev/api/films/1/, http://swapi.d... |  19.0 |
|    1 |          C-3PO |     112BBY | [http://swapi.dev/api/films/1/, http://swapi.d... | 112.0 |
|    2 |          R2-D2 |      33BBY | [http://swapi.dev/api/films/1/, http://swapi.d... |  33.0 |

Finally, our dataset is ready. So, who is the oldest  and youngest character? Let's find out: 

```python
oldest = subset[subset.year == max(subset.year)]
youngest = subset[subset.year == min(subset.year)] 
print(f'The oldest charecter is {oldest.name.values[0]} who was born in {oldest.year.values[0]} BBY. \nAnd the youngest character is {youngest.name.values[0]} who was born in {youngest.year.values[0]} BBY.')
```

```python
The oldest charecter is Yoda who was born in 896.0 BBY. 
And the youngest character is Wicket Systri Warrick who was born in 8.0 BBY.
```

Wow, Yoda is really old. No wonder why he is so wise! 

# Find the films that the Yoda appeared in

Since the `films` column contains a list of URLs of movies, we can extract the titles of these movie as follows: 

```python
#the following list comprehension pulls the data from API for each URL in the films column, converts it to JSON format, 
#and pulls the title of the movie. 

[j['title'] for j in [requests.get(i).json() for i in subset.films[oldest.index.values[0]]]]
```

```python
['The Empire Strikes Back',
 'Return of the Jedi',
 'The Phantom Menace',
 'Attack of the Clones',
 'Revenge of the Sith']
```

Yoda, my favorite Star Wars character, appeared in five Star Wars movies. No wonder that my favorite Star Wars movies were with Yoda in them. 

So, wise he is! Let me end this post with his quote: 

`Try not. Do or do not. There is no try` -Yoda

May the Force be with you. 