---
layout: post
title: Predicting Future Movie Gross
---

![]({{ site.baseurl }}/assets/images/02-banner.jpg)
{: .image.featured}

The second project I worked on is trying to predict the future of the US domestic film industry by looking at the total gross of top 100 films. I chose top 100 because it is where the majority of the total gross come from. In addition I can gather the information of the top movies in addition to the total gross. The first part of the project involve scrapping for data online. I used Selenium because it give a nice interface that simulates user interaction with a website. More specifically the xpath function allow very good filter to find the information on each page. The main source of information I gathered is from moviedojo.com for the gross of top 100 films from 1982 to 2015. Other information are related to the factors I think influences the total gross, including the total US population, the consumer price index, the change in gdp, unemployment, and the movie price over the years.

![]({{ site.baseurl }}/assets/images/02-gross.png "Total Gross")

This plot shows the total gross as a function of time, the trend is clearly increasing every year. Does this mean the future is bright for the film industry?  

![]({{ site.baseurl }}/assets/images/02-normalized.png "Normalized")
![]({{ site.baseurl }}/assets/images/02-ticket-price.png "Ticket Price")

The picture changes when normalizing the gross by two factors that increases almost constantly over the years, the total US population, and the Consumer Price Index. More total population would naturally increase the people who might watch a movie, and so does the consumer price index, which is a proxy for inflation. In fact the average ticket price for movies approximately follows closely with the Consumer Price Index.  

![]({{ site.baseurl }}/assets/images/02-economic.png "Economic")

The values of the normalized gross varies widely between years. I have some theories of what contribute to this, the top two are the economic conditions of the current year, perhaps people like entertainment when the economy is good, or alternatively people want their mind off their regular lives when the economy is bad. The second is the top grossing blockbusters, depending on the year, a significant portion of the box office is the biggest blockbusters, and depending on how well they perform, perhaps that has a big influence on the total gross. The last one is an unknown trend over the years that might affect the total gross, this value will be modelled purely based on the time (year) variable.  

![]({{ site.baseurl }}/assets/images/02-movie-buff.png "Movie Buff")

I plotted the log y-axis scaled top 100 gross plot of movies for each year, with purple being 1982 and red being 2015, the trend shows almost a linear relation for movies which grossed in the 20 to 100 range. This trend is fitted with a simple linear model to yield a constant multiplied by 0.98 to the power of the rank. I termed this the Movie Buff Model, where the gross of each movie can be estimated by taking 0.98 times the previous value. An interesting feature of this model is that it does not include the top blockbuster, so using the method the total gross of each year can be estimated without the influence of the top grossing movies.  

![]({{ site.baseurl }}/assets/images/02-blockbuster.png "Blockbusters")

One can also make plot of the predicted gross for each year against the estimated blockbuster gross (here estimated by subtracting the Movie Buff prediction from the total gross). This plot shows movies that have low blockbuster and low total gross on the lower left, high blockbuster and high gross on the top right, and interestingly some years with high blockbuster but with low total gross on the lower right. This plot does not show a clear linear relation, thus we can say blockbusters are not a very good predictor of total gross, although there appears to be a somewhat direct relation between the two.  

![]({{ site.baseurl }}/assets/images/02-fit.png "Final Fit")

Finally fitting total gross with independent variables of GDP change (this is a more direct predictor of the economy than unemployment), it can be shown that a cubic time variable give the best fit with evenly distributed residuals. This is certainly not looking very good for the movie industry as a whole, where the total gross is predicted to go down in the next few years. Although the down trend is still higher than the low value of the 1980's an early 1990's, it is still too early to tell whether this is a temporary or a permanent phenomenon.  


