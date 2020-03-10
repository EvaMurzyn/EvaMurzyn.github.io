---
layout: post
title: "Stormy season!"
date: 2020-03-05 08:44:20
description: Analysing storm hashtags on Twitter # Add post description (optional)
img: stormy-season.jpg  # Add image post (optional)
---


This February has probably been the wettest and windiest month since I moved to Scotland, back in 2004. [Met Office](https://www.metoffice.gov.uk/about-us/press-office/news/weather-and-climate/2020/2020-winter-february-stats) has estimated the rainfall was somewhere between 150% to 450% of the usual February values across the UK. A lot of this was courtesy of some fierce Atlantic storms rolling over the country, including Brendan, Ciara and Darren, and a host of other unnamed depressions.

On one of the last days of Storm Dennis, I attended an [R-Ladies workshop](https://www.meetup.com/rladies-edinburgh/events/268430176/) where University of Glasgow’s Anna Herschel gave a great demo of using the “rtweet” package for scraping Twitter data, and "tidytext" for running simple sentiment analysis on the resulting information. If you'd like, you can find her workshop materials at [Hack Your Data Beautiful](https://psyteachr.github.io/hack-your-data/scrape-twitter.html).

I wanted to apply and expand those skills, and started thinking about looking at one of the storm hashtags that were used across Twitter to talk (and complain) about the weather. In the past, social media data has been used to track the spread of [flu](https://www.sciencedaily.com/releases/2017/05/170509121952.htm) and [public protests](https://arxiv.org/ftp/arxiv/papers/1805/1805.00358.pdf).

Unfortunately, my timing was wrong, and I didn’t manage to capture a ‘real’, Met-Office named storm. However, as potential Atlantic depressions were approaching the coast, media was quick to give them names anyway, leading to the emergence of the “Storm Ellen” hashtag. I scraped all original tweets using that hashtag across 2 weeks, between the 15th and 29th of February, and started asking questions.
 

## How did the hashtag develop?

Despite the original Storm Ellen warnings in papers on the 14th and 15th of February, the hashtag exploded only on Saturday 22nd of February, over a week after the initial use.
![StormEllen Tweets](/assets/img/tweets.jpg) <!-- .element height="40%" width="40%" -->
While it's hard to fully understand why hashtags rise and fall, 22nd of February was pretty terrible weather-wise, and there were numerous [news reports](https://www.theguardian.com/uk-news/2020/feb/22/heavy-showers-bring-fresh-flooding-parts-uk) of snow, rain and flooding across the UK. 
  

## What were people talking about?
I had a look at the most frequently used words in the #StormEllen tweets. Overall, other storm names (Ciara, Dennis and Jorge) seemed to be mentioned most frequently, with people both comparing the weather across different storms, or just using as many weather-related hashtags as they could fit in.

After these were removed, these were left:
![StormEllen word cloud](https://github.com/EvaMurzyn/EvaMurzyn.github.io/blob/master/assets/img/clouds.jpg) <!-- .element height="40%" width="40%" -->

Following Anna's workshop, I ran a quick sentiment analysis, and it turned out that overall, the tone of the tweets was negative, and leaning heavily towards anger at the continuing bad weather. 

![StormEllen sentiment analysis results](https://github.com/EvaMurzyn/EvaMurzyn.github.io/blob/master/assets/img/sentiment.jpg) <!-- .element height="40%" width="40%" -->  

## What storm related phenonomena were being mentioned?

The word cloud and sentiment analysis were fun, but I wanted to get a clearer idea of what exactly was being mentioned. Was it the rain? The wind? The flooding, and associated damage?
  
I created some ad-hoc lists of words related to 4 types of weather phenomena associated with storms. The lists are incomplete, and I’m thinking about building a more comprehensive dictionary of interest for future weather related projects.

-   Precipitation: rain, sleet, snow, drizzle, etc.
    
-   Wind: breeze, gale, hurricane, stormy, etc.
    
-   Water: river, waves, tide, stream, etc.
    
-   Damage: floods, destroyed, cancelled, submerged, etc.
      
I calculated the average number of mentions of these 4 categories per tweet, and plotted them:
![Mentions of different weather phenomena](https://github.com/EvaMurzyn/EvaMurzyn.github.io/blob/master/assets/img/mentions.png) <!-- .element height="40%" width="40%" -->

While wind terms were used fairly evenly across time, mentions of rain and damage seemed to peak around 20th and 24th of February. 

## Were the mentions related to the severity of the weather?

 I grabbed February weather records from [WeatherUnderground](https://www.wunderground.com/), using the  data from London, Edinburgh and Glasgow stations to try to get an overall UK-wide estimate of wind speed and precipitation during the hashtag's existence. 

I mapped the changes in these two parameters onto the weather mentions, and ran some correlations,  but sadly, there didn't seem to be a clear-cut relationship. 

This is the data for maximum wind speed:
![Wind speed and mentions of winds and damage](https://github.com/EvaMurzyn/EvaMurzyn.github.io/blob/master/assets/img/wind_speed.png) <!-- .element height="40%" width="40%" -->

And this is the data for total precipitation:
![Mentions of precipitation, and rain, water and damage](https://github.com/EvaMurzyn/EvaMurzyn.github.io/blob/master/assets/img/precipitation.png) <!-- .element height="40%" width="40%" -->
  
It's possible that I could find something with a longer data stretch - 14 data points is generally not enough to uncover weak to medium correlations. I'd be also interested in looking at possible delays in mentions - it's possible that people are tweeting about damage a day or two after it happens, as news spreads across communities.

## Conclusions

This was a fun little project, and it helped me apply my workshop skills in a new context. Twitter is a such a good place to go for data on natural and social phenomena, such as hurricanes, earthquakes and social movements, and I will come back to it to refine my approach next time a stormy month comes along.
However, it's worth remembering that there is [no guarantee that people are telling the truth online](https://www.npr.org/sections/alltechconsidered/2015/04/20/400125638/social-media-can-help-track-tornadoes-but-was-that-tweet-real?t=1583439700950). Between bot accounts hijacking popular hashtags to push their message, and people making things up for attention and laughs, social media data needs to be taken with a solid pinch of salt.

Image used is by [NOAA Photo Library](https://www.flickr.com/photos/noaaphotolib/27330284504/in/album-72157624929569729/)
> Written with [StackEdit](https://stackedit.io/).
