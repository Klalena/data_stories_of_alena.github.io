---
layout: post
title: Trends of Malaria Cases Worldwide 
subtitle: With Interactive Visualizations 
cover-img: /assets/img/malaria/mosquito_BW.jpg 
thumbnail-img: /assets/img/malaria/malaria.jpg
tags: [Malaria, Interactive Visualizations, Plotly, Bokeh]

---

In this post, I will explore a few  trends of Malaria worldwide from 2010 to 2015 using data from [Our World in Data](https://github.com/rfordatascience/tidytuesday/tree/master/data/2018/2018-11-13). I will utilize the beauty and effectiveness of interactive visualizations created with `Plotly` and `pandas_bokeh`  in Python to illustrate how the number of malaria cases and deaths changed through time. In addition, I will highlight age and income group that succeeded the most in the fight against malaria from 2010 to 2015. 

## About [Malaria](https://www.who.int/news-room/fact-sheets/detail/malaria)

Malaria is a disease caused by *Plasmodium* parasites, which is mostly transmitted  by mosquitoes (infected female *Anopheles* mosquitoes). Even though malaria is a curable and preventable disease,  it can be fatal when not diagnosed early and treated properly. The distribution  of malaria cases and deaths vary greatly among geographic regions and age groups.  The majority of cases and deaths are in the African region ([> 93% as of 2018](https://www.who.int/news-room/fact-sheets/detail/malaria)), and children under 5 years old are the most susceptible age group to contract and die from malaria. According to the World Health Organization (WHO), in 2018 alone, there were more than *200 million* malaria cases and  more than *400 thousand* deaths worldwide. Although these numbers are alarming, they are significantly lower than they were a decade ago, which mainly can be attributed to the WHO Malaria Elimination initiative, rigorous nationwide  policies on malaria treatment and prevention, and the vaccine against malaria. 



## 1️⃣ Malaria Cases Worldwide Reduced Substantially from 2000 to 2015 



The maps below show the countries with malaria cases in 2000 and 2015. The darker the color of the country, the more malaria incidents it had, where the darkest color indicates countries with more than 600 cases per 1000 population at risk. As can be vividly seen from the maps, the 2000 map is considerably darker than that of 2015, particularly with regards to the African region.													

### 2000 

![Malaria cases in 2000](../assets/img/malaria/malaria_cases_2000.gif)



### 2015 

![Malaria cases in 2015](../assets/img/malaria/malaria_cases_2015.gif)



For example, the table below shows a sizable reduction in the number of cases of the top 3 countries (in the number of cases) through time. 

|    Country    | Cases in 2000 | Cases in 2015 |
| :-----------: | :-----------: | :------------ |
|   Ethiopia    |      662      | 59            |
| Burkina Faso  |      621      | 389           |
| Cote d'Ivoire |      525      | 349           |

👩‍💻 Tips: 

- I used `pandas_bokeh` to create the maps. You can find the code here. 

- To create a `gif` file to show the interactivity of the maps, I used [Giphy](https://giphy.com/). 

  

## 2️⃣ Number of Malaria Incidences Almost Halved in Sub-Saharan Africa 



From the maps above, we saw that Malaria cases reduced greatly. However, what region experienced *the highest drop* in malaria cases in the 15-year period? Looking at the graph below, we can see that relative to the world and other regions, Sub-Saharan Africa had a sharp reduction in malaria cases. It can be partially explained by  state and non-profit initiatives aiming to eliminate malaria. 

<iframe width="770" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/4.embed"></iframe>

👩‍💻 Tips: 

- These are interactive visualization, where you can hover over a specific region to learn more about a data point. To see one or a few particular groups with a rescaled y-axis, you can unselect unnecessary groups in the legend. Furthermore, you can explore many more options in the top right corner of the graph. 

  

- To create these visualizations, I used `plotly` backend (`pd.options.plotting.backend = "plotly"`)

  

- Wondering how I embedded these  `plotly` graphs on my website 🤔? Check out this [video](https://www.youtube.com/watch?v=kxPZV9ileKI). 



## 3️⃣ Low Income Countries More Than Halved their Malaria Cases 

Looking at the countries grouped by income, we can see that the world and three income groups have a decreasing trend in the number of malaria cases; however, the low income group stands out in its sharp drop in cases in 2000-2015. This could be attributed to the economic growth in some of those countries, increased help from international communities, and robust prevention policies.



<iframe width="770" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/9.embed"></iframe>





## 4️⃣ Sharp Decrease in Average Number of Deaths From Malaria for Children Under 5

As mentioned earlier, children under 5 years old are the most vulnerable group to contract malaria and die from it. However, as can be seen from the graph below, there was a promising reduction in the number of deaths since 2003. 

<iframe width="770" height="500" frameborder="0" scrolling="no" src="//plotly.com/~alena3/1.embed"></iframe>



Despite a significant improvement in the reduction of malaria cases and deaths, much work needs to be done to accomplish [the WHO goal](https://www.who.int/malaria/areas/global_targets/en/#:~:text=The%20Strategy%20sets%20ambitious%20but,in%20at%20least%2035%20countries) of reducing malaria cases and mortality rates by 90% or more by 2030. 



**References:** 

[WHO](https://www.who.int/news-room/fact-sheets/detail/malaria)



