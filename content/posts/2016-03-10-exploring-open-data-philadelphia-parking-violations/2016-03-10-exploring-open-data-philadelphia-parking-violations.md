---
title: Exploring Open Data - Philadelphia Parking Violations
author: Jacob Rozran
date: '2016-03-10'
slug: exploring-open-data-philadelphia-parking-violations
categories:
  - Open Data
  - Data Analysis
  - Data Engineering
tags:
  - data engineering
  - data analysis
  - data visualization
  - open data
  - tableau
  - cartoDB
---

### Introduction

A few weeks ago, I stumbled across [Dylan Purcell's](https://twitter.com/dylancpurcell) 
article on [Philadelphia Parking Violations](http://data.philly.com/philly/parking/). 
This is a nice glimpse of the data, but I wanted to get a taste of it myself. I 
went and downloaded the entire data set of 
[Parking Violations in Philadelphia](https://www.opendataphilly.org/dataset/parking-violations) 
from the [OpenDataPhilly website](http://opendataphilly.org/) and came up with a 
few questions after checking out the data:

How many tickets in the data set?

* What is the range of dates in the data?
* Are there missing days/data?
* What was the biggest/smallest individual fine? What were those fines for? Who 
issued those fines?
* What was the average individual fine amount?
* What day had the most/least count of fines? What is the average amount per day
* How much $ in fines did they write each day?
* What hour of the day are the most fines issued?
* What day of the week are the most fines issued?
* What state has been issued the most fines?
* Who (what individual) has been issued the most fines?
* How much does the individual with the most fines owe the city?
* How many people have been issued fines?
* What fines are issued the most/least?

And finally to the cool stuff:

* Where were the most fines? Can I see them on a heat map?
* Can I predict the amount of parking tickets by weather data and other factors 
using linear regression? How about using Random Forests?

### Data Insights
This data set has 5,624,084 tickets in it that spans from January 1, 2012 through 
September 30, 2015 - an exact range of 1368.881 days. I was glad to find that 
there are no missing days in the data set.

The biggest fine, $2000 (OUCH!), was issued (many times) by the police for "ATV 
on Public Property." The smallest fine, $15, was issued also by the police 
"parking over the time limit." The average fine for a violation in Philadelphia 
over the time range was $46.33.

The most violations occurred on November 30, 2012 when 6,040 were issued. The 
least issued, unsurprisingly, was on Christmas day, 2014, when only 90 were 
issued. On average, PPA and the other 9 agencies that issued tickets (more on 
that below), issued 4,105.17 tickets per day. All of those tickets add up to 
$190,193.50 in fines issued to the residents and visitors of Philadelphia every 
day!!!

Digging a little deeper, I find that the most popular hour of the day for 
getting a ticket is 12 noon; 5AM nets the least tickets. Thursdays see the most 
tickets written (Thursdays and Fridays are higher than the rest of the week; 
Sundays see the least (pretty obvious). Other obvious insight is that PA licensed 
drivers were issued the most tickets.

Looking at individuals, there was one person who was issued 1,463 tickets 
(thats more than 1 violation per day on average) for a whopping $36,471. In 
just looking at a few of their tickets, it seems like it is probably a delivery 
vehicle that delivers to Chinatown (Tickets for "Stop Prohibited" and "Bus Only 
Zone" in the Chinatown area). I'd love to hear more about why this person has 
so many tickets and what you do about that...

**1,976,559 people** - let me reiterate - nearly **2 million unique vehicles** 
have been issued fines over the three and three quarter years this data set 
encompasses. That's so many!!! That is 2.85 tickets per vehicle, on average (of 
course that excludes all of the cars that were here and never ticketed). That 
makes me feel much better about how many tickets I got while I lived in the city.

And... who are the agencies behind all of this? It is no surprise that PPA 
issues the most. There are 11 agencies in all. Seems like all of the policing 
agencies like to get in on the fun from time to time.

| Issuing Agency | count |
|----------------|-------|
| PPA | 4,979,292 | 
| PHILADELPHIA POLICE | 611,348 |
| CENTER CITY DISTRICT | 9,628 |
| SEPTA | 9342 |
| UPENN POLICE | 6,366 |
| TEMPLE POLICE | 4,055 |
| HOUSING AUTHORITY | 2,137 |
| PRISON CORRECTIONS OFFICER | 295 |
| POST OFFICE | 121 |
| FAIRMOUNT DISTRICT | 120 |

### Mapping the Violations

Where are you most likely to get a violation? Is there anywhere that is completely 
safe? Looking at the city as a whole, you can see that there are some places 
that are "hotter" than others. I 
[played around in cartoDB to try to visualize this as well](https://rozran00.cartodb.com/viz/ea4ebb4e-e7c0-11e5-8939-0e5db1731f59/public_map), 
but tableau seemed to do a decent enough job (though these are just screenshots).

![parking_tickets_macro](/img/parking_tickets_macro.png)

Zooming in, you can see that there are some distinct areas where tickets are 
given out in more quantity.

![parking_tickets_micro](/img/parking_tickets_micro.png)

Looking one level deeper, you can see that there are some areas like Center City, 
east Washington Avenue, Passyunk Ave, and Broad Street that seem to be very 
highly patrolled.

![parking_tickets_zoom](/img/parking_tickets_zoom.png)

### Summary

I created the above maps in Tableau. I used R to summarize the data. The R 
scripts, raw and processed data, and Tableau workbook can be found in 
[my github repo](https://github.com/jrozra200/philly_parking_ticket_analysis).

[In the next post, I use weather data and other parameters to predict how many tickets will be written on a daily basis](https://www.jakelearnsdatascience.com/posts/exploring-open-data-predicting-the-amount-of-violations/).