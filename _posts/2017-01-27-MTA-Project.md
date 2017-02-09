---
layout: post
title: Analyzing New York Subway Data
---

![]({{ site.baseurl }}/assets/images/01-banner.png)
{: .image.featured}

This project is on how to analyze the New York Subway turnstile data and presenting the results to a hypothetical client interested using the information for their business. Despite other distraction and the time constraint, I was able to complete a cool exploratory analysis of the data.

![turnstile]({{ site.baseurl }}/assets/images/01-turnstile.png "NY MTA Turnstile")

The turnstile data is pretty messy, the table consists of a list of values for a particular turnstile at a particular station at a time. New time data are updated about every 4 hours. The output values of this data are the entry and exit cumulative counts for that particular turnstile/station/time combination. What makes this data messy is the fact that the raw number of entries/exits are computed by subtracting the value at one time by the value of the previous time. In addition, sometimes the turnstils reset their values, or their value can be overflow back down to zero. The data is also incomplete, some dates and times might be missing or not sync'd between stations/turnstiles.

![Gif]({{ site.baseurl }}/assets/images/01-movie.gif "NY MTA Visualization")

This data can be plotted using basemap and NYC Boroughs shapefile, and with the size of each station corresponds to the log daily traffic over time. I had originally wanted to combine this data with another source such as the census to find interesting combinations of information. However, forces outside of my control decided the only data source should be the turnstile data. This reduces the complexity of the information available, but a more in depth analysis of the turnstile data can be performed. The results of this analysis can tell us how busy each station is and in addition I want to find out about the type of station from just the time data. The possibilities are stations near residential area, which should have high traffic entering in the morning and exiting in the afternoon, or stations near businesses which have high traffic exiting in the morning and entering in the afternoon, and lastly touristy stations which might have smaller time of the day, weekday/weekend variations, but has a larger seasonal variability.

![FFT]({{ site.baseurl }}/assets/images/01-FFT.png "Fourier Transform")

The method I chose to use is Fast Fourier Transform on the Entries and Exits for each station. The data, despite its difficulties is very good for Fourier Transforms, since the sampling time is at regular intervals, and the data or signal is expected to be periodic. From the plot, it seems like there are two frequencies corresponding to periods of 7 and 14 times a week. This clearly is where the rush hour is happening. From the transform we can then extract the phase (time shift) and amplitude (amount) for both entries and exits of all stations.

![Ratio]({{ site.baseurl }}/assets/images/01-ratio_compare.png	"Ratio Compare")

As a starting point of analysis, we can look at the ratio of Entry and Exit amplitudes for the daily period of each station. As can be seen in the graph, there appears to be a positive relation between them. This is promising, as we expect daily commutes of each station to be proportional, people generally enter and exit at the same station during commutes.

<img src={{ site.baseurl }}/assets/images/01-phase_comp.png width="100%"/>

Here is a plot of the phase of the entry and exit daily period for stations. This method appears able to be filtering out the residential and business stations. In the morning, people are entering stations near their residence and exiting near the business district, while the reverse is true in the afternoon.

![Subway]({{ site.baseurl }}/assets/images/01-subway.gif	"Subway")

If I had more time or more help on the project I would include more time data to include time frames of a month or even up to a year. This would be able to show more weekly and seasonal features. In addition, the output of the Fourier Transform can be further interpreted to better determine the peak information (i.e. peak integration instead of peak value).
