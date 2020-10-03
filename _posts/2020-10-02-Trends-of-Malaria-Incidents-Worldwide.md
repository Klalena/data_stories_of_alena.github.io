---
layout: post
title: Trends of Malaria Incidents Worldwide 
subtitle: With Interactive Visualizations 
cover-img: /assets/img/malaria/mosquito_BW.jpg 
thumbnail-img: /assets/img/malaria/malaria.jpg
tags: [Malaria, Interactive Visualizations, Plotly, Bokeh]

---

In this post, I will explore a few insightful trends of Malaria worldwide from 2010 to 2015 using data from [Our World in Data](https://github.com/rfordatascience/tidytuesday/tree/master/data/2018/2018-11-13). I will utilize the beauty and effectiveness of interactive visualizations created with `Plotly` and `pandas_bokeh`  in Python to illustrate how the number of malaria cases and deaths changed through time. In addition, I will highlight age and income group that succeeded the most in the fight against malaria from 2010 to 2015. 

## About [Malaria](https://www.who.int/news-room/fact-sheets/detail/malaria)

Malaria is a disease caused by *Plasmodium* parasites, which is mostly transmitted  by mosquitoes (infected female *Anopheles* mosquitoes). Even though malaria is a curable and preventable disease,  it can be fatal when not diagnosed early and  treated properly. The distribution  of malaria cases and deaths vary greatly among geographic regions and age groups.  The majority of cases and deaths are found in the African region ([> 93% as of 2018]((https://www.who.int/news-room/fact-sheets/detail/malaria))), where children under 5 years old are the most susceptible age group to contract and die from malaria. According to the World Health Organization, in 2018 alone there were more than 200 million malaria cases and  more than 400 thousand deaths worldwide. Although these numbers are alarming, they are significantly lower than they were a decade ago, which mainly can be attributed to the WHO Malaria Elimination initiative, rigorous nationwide  policies on malaria treatment and prevention, and the vaccine against malaria. 



## 📊 Malaria Cases Worldwide in 2000 vs 2015 



The maps below show the countries with malaria cases in 2000 and 2015. The darker the color of the country, the more malaria incidents it had, where the darkest color indicates countries with more than 600 cases per 1000 population at risk. As can be vividly seen from the maps, the 2000 map is considerably darker than the 2015 map, particularly the African region.													

### 2000 

![Malaria cases in 2010](../assets/img/malaria/malaria_cases_2010.gif)





### 2015 

![Malaria cases in 2015](../assets/img/malaria/malaria_cases_2015.gif)



For example, the table below shows a sizable reduction in the number of cases of the top 3 countries (in the number of cases) during 15 years. 

|   Country    | Cases in 2000 | Cases in 2015 |
| :----------: | :-----------: | :------------ |
|    Turkey    |     1741      | 0             |
|   Ethiopia   |      662      | 59            |
| Burkina Faso |      621      | 389           |
|              |               |               |



Nigeria (25%), the Democratic Republic of the Congo (12%), Uganda (5%), and Côte d’Ivoire, Mozambique and Niger (4% each).

### Low-Income Countries More Than Halved the Malaria Cases from 2000 to 2015

<iframe width="900" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/9.embed"></iframe>

### Sharp Decrease in Average Number of Deaths From Malaria for Children Under 5

<iframe width="900" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/1.embed"></iframe>

### Number of Malaria Incidences Almost Halved in Sub-Saharan Africa from 2000 to 2015

<iframe width="900" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/4.embed"></iframe>

**References:** https://www.who.int/news-room/fact-sheets/detail/malaria



