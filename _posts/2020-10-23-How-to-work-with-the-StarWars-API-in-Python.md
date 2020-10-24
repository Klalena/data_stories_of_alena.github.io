---
layout: post
title: How to work with the StarWars API in Python
subtitle: Using `requests` package 
cover-img: /assets/img/StarWars_API/yoda_cover.jpg
image: /assets/img/StarWars_API/yoda.jpg
tags: [StarWars API, REST API]

---

As more companies provide access to their data through their APIs, it became increasingly common to use APIs to retrieve data. This tutorial will show how to get data from the [`SWAPI(The Star Wars API)`](https://swapi.dev/documentation) in Python using `requests` package and how to answer the following question: 

**Who is the oldest character in the Star Wars Universe and in which films it was appeared?**

#  Get Data from the Star Wars API 

```python
import requests
url = 'http://swapi.dev/api/'
response = requests.get(os.path.join(url, 'people/'))
data = response.json()
```





sample data 

conversion to json format 

Who is the oldest charcter? 

Wondering who is the youngest? 

- include image (if possible)

In which movies Yoda was shot?  