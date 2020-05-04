---
layout: post
title: "Looking at COVID-19 mobility data"
date: 2020-05-04 17:44:20
description: Analysing Google COVID-19 mobility reports for UK
img: covid-mobility.jpg  
---


There are thousands of data science posts about COVID-19 - models, predictions, graphs, simulations, of good, bad or questionable quality. We're all trying to understand and quantify this pandemic, both to keep sane and to avoid the lockdown boredom.

One of the things that caught my interest was the [mobility data released by Google](https://www.blog.google/technology/health/covid-19-community-mobility-reports?hl=en). The data tracks 6 different types of mobility:
 - Retail and recreation
 - Grocery and pharmacy
 - Parks
 - Transit stations
 - Workplaces
 - Residential

Each of the values represents a percentage change from baseline, although Google is very vague on what the baseline is. It could be previous year's statistics, as that would mean that the values would be responsive to seasonal changes. Initally, Google only shared pdfs of reports, but now they've started supplying it in a handy csv file, with data for the whole world, starting mid-February.

I decided to extract the UK data, broken down into regions, and map the changes in mobility across time using R.

 The first challenge of this project was the fact that Google region names were not always matched with the {sf} package generated UK region map that I was hoping to use. After looking for other mapping solutions, I decided to bite the bullet and create a manual key that would match the mapping and mobility regions. Most of the mismatches were caused by simple differences such as Google's "Aberdeen City" vs sf "Aberdeen", or Google's "Windsor and Maidenhead" mapping to "Royal Borough of Windsor and Maidenhead". However, some were trickier and required Wikipedia sleuthing to match up - usually due to changes in administrative regions over time, or Google reporting on larger aggregate regions that sf maps break down into their component areas. The most frustrating part of this exercise was Bristol, which exists in sf maps, but not in the Google data, and its Wikipedia page gives no hint as to what other administrative unit it's part of - it only states that Bristol lies between Gloucestershire and Somerset. I ended up matching it to Gloucestershire in the end, but I'm sure there is a better solution out there.

The resulting [key data frame](https://github.com/EvaMurzyn/Blog_data/blob/master/2020-05-04-Covid_mobility/Data/uk_sf_map_data_key.csv) is now available on my github, so if you'd like to give this a go, you can avoid re-doing the work. The *'name'* column represents the sf map name, while the *'google_name'* is the corresponding Google mobility report area.

Once I had the key, I dove into learning the {tmap} package, which promised an integrated solution for creating animations. After following an excellent tutorial on [R Spatial Mapping](https://spatialanalysis.github.io/lab_tutorials/4_R_Mapping.html), I ended up with a short code that could be used to map my variables.

    anim1 <- UK_late %>%
      tm_shape() +
      tm_fill("retail_and_recreation_percent_change_from_baseline", title = "Retail and Recreation Mobility", 
                  palette = color_hex_7, colorNA = NULL) +
      tm_borders(col = "white", lwd = 0.5) +
      tm_layout(legend.outside = TRUE, legend.outside.position = "right", legend.title.size = 4) +
      tm_facets(along = "date")
    
    tmap_animation(anim1, filename = "retail_UK_anim.gif", width = 1000, height = 1000,
                   delay = 50, restart.delay = 200)

I also created a custom colour palette using the [Data Colour Picker](https://learnui.design/tools/data-color-picker.html) tool.
 Applying this code to all the variables gave me these 4 animated maps:

**Retail and Recreation **
![Retail mobility report](/assets/img/retail_UK_anim.gif)

**Grocery and Pharmacy**
![Grocery and Pharmacy](/assets/img/grocery_UK_anim.gif)

**Transit Stations**
![Transit Stations](/assets/img/transit_UK_anim.gif)

**Workplaces**
![Workplaces](/assets/img/workplace_UK_anim.gif)

If you'd like to give this a go with later Google data, or when choosing different date values, be aware that the *tm_fill()* colour mapping function decides on the number of bins automatically, and if the number of colours you specify doesn't match the breakdown, it ends up rendering incorrectly. You may need to do some manual tweaking with the scales.

**The big picture**
You probably have noticed the periodic changes in the graphs, with some days showing more limited mobility than others. To look at the overall patterns, I plotted the summary data for the whole UK to show a timeline of mobility from February to 26th of April.

![Timeline graph](/assets/img/timeline.png)

In this graph, the points on lines highlight the weekends, which tend to deviate from the weekday pattern. Additionally, I marked the start of social distancing orders (16th of March) and lockdown (announced on 23rd of March) using annotation tools to showcase how behaviour changed once official guidance was given. 

It's wonderful to see how people did the right thing, and stayed at home to minimise the risk of the illness spreading. 

Title image by [ExpectGrain on Flickr](https://www.flickr.com/photos/spedster/22614419698)

Code and source files can be found on my [GitHub](https://github.com/EvaMurzyn/Blog_data/tree/master/2020-05-04-Covid_mobility).
> Written with [StackEdit](https://stackedit.io/).
