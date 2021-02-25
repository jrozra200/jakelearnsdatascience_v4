---
title: "What is Data Science?"
author: "Jacob Rozran"
date: '2021-02-24'
slug: what-is-data-science
categories: Data Science
tags: data science
---

If you search for data science or data scientist, you get a lot of 
[pretty Venn Diagrams](https://www.google.com/search?q=data+science+venn+diagram)
or [cool infographics](https://www.google.com/search?q=modern+data+scientist) 
that happily point out that this is a multidisciplinary field that includes 
statistics, problem solving, computer science and engineering, data 
visualization, communication, and domain expertise.  

Beyond those graphics in your search, you will find dense articles, blog posts, 
and flashy ads about the latest machine learning (ML) or artificial 
intelligence (AI) tool and the custom fitted hardware to enable them. Hell, even 
Apple's newest models of iPhone have custom hardware and AI built into them. 

While I have spent a lot of time working on all of the skills above and trying 
to digest and enjoy some of the new hotness in ML and AI, I think that this 
tends to make data science less approachable and confuses people about what data 
science really is all about.

**In the end, data science is about finding data supported answers to real-life problems.** 
While sometimes it does seem enticing (and it certainly can seem 
impressive on a resume or in talking to your friends, family, and strangers) 
to jump straight to the hardcore predictive end of the data science spectrum, 
data science is a long and iterative path. Very generally speaking, data science 
is inclusive of issue discovery, data discovery, data visualization and story 
telling, advanced analytics, and testing and predictive analytics, and ethics 
(stop when it makes sense; repeat if necessary).

<p align="center">

![Data Science Lifecycle](ds_lifecycle.jpg)

</p>

# THE DATA SCIENCE LIFECYCLE

## DATA SCIENCE IS ALWAYS ITERATION AND COMMUNICATION

To begin with, data science is 
inherently an communicative process. A data scientist must be in constant 
communication with the relevant stakeholders. This can be the executive asking 
questions, the DBA who knows the data best, the customer who is being affected 
by your model's decision, the person who was handed a copy of your presentation 
from 6 months ago, etc. In effect, I work for all of these people and need their 
input to be successful. 

Also, as you learn while progressing through the lifecycle, you may need to go 
back a step (or more) and update (again). 

## DATA SCIENCE IS ALWAYS ISSUE DISCOVERY

It is easy to ask a question: "How many users do we have on our platform?" or 
"What should we expect in sales for this holiday season?" 

It takes everything I have, every time, to not go run off and find an answer 
right away. You must understand the nuance to the question and the context in 
which the question is being asked. 

For the first question posed above: What type of users? Web users? Active users? 
If it is active users, active since when? Paying Customers? Anyone who has ever 
logged in? You get the point. 

Once you have clarified the question (which requires iteration with your 
stakeholder), zoom out. Why is this person asking that question? What are they 
going to do with that information? Is it worth it for me to spend a ton of 
effort on it? This all informs how you tackle the problem and the lens through
which you look at the data. If any of it is unclear, go back and ask.

## DATA SCIENCE IS ALWAYS DATA DISCOVERY

Once the problem and context are clear, you need data to solve your problem. 
This data is never what you are expecting. The real world is messy and so too is 
the data. There will be nonsensical values, missing values, duplicate values, 
etc. Data changes over time and is sometimes in weird formats. 

Combing through the data to find all of this can be tedious and it almost 
certainly will require reaching out to someone else for more information. A 
good exploratory data analysis is absolutely essential for any downstream steps 
to be successful. 

You do not want to proceed to the next step without a comprehensive 
understanding of the data. From experience, I can tell you it does not feel good 
to spend hours working on a report to have the stakeholder blow it up in the 
first minute because you presented the data incorrectly. 

## DATA SCIENCE IS MOST OF THE TIME DATA VISUALIZATION AND STORY TELLING

descriptive
data presentation - decks and dashboards
visualizations that are clean and clear
story telling
explaining complex nuance in simple language but not offending anyone's intelligence
iterate with the "client" to understand what is expected and what is surprising

Side note: Data science is NOT pie charts or 3d effects. Period. 

## DATA SCIENCE IS OFTEN ADVANCED ANALYTICS

things may stick out, so you do a deep dive on those things
this is your advanced analytics
iterate with the "client" to identify causes for these weird things
this may require you to get more data and start back at the EDA and descriptive analytics

## DATA SCIENCE IS SOMETIMES TESTING AND PREDICTIVE ANALYTICS

once you and your "client" have a good hold on what is happening, then you can start to do predictive analytics
this _can_ be cool stuff, like random forests, GBM, neural networks, but regression is often easier to implement and better to understand
start small and do tests - A/B testing to see if your prediction moves the needle in a meeaningful way
then roll it out in scale
all the while, iterate with your "client" to make sure things are working as expected

prediction comes in a lot of flavors; in marketing you are trying to predict who is the most apt to buy your thing
in credit you are predicting who will (or won't) pay you back
in computer vision, you are predicting what an object is

## DATA SCIENCE IS ALWAYS ETHICS

It is not in the lifecycle diagram, but it really should be. The hard part about 
adding it is that it needs to live at every step of the process. Data scientists 
often get access to sensitive data and are asked to make powerful tools that 
affect real people in real ways. Knowing what your outputs are being used for 
and why they are being used is necessary to start, then knowing when (and 
speaking up) that crosses an ethical boundary. We all come with our biases and 
need to make sure we are not propagating them through our work - it is very easy 
in data science to forget this because you are removed from the actual decision.

Use data for good. Primum non nocere. First do no harm.

# SO... WHAT IS DATA SCIENCE? 

Data science is a lot of things, but primarily it is problem solving. It fits 
within every business unit and in every industry. Many people are doing data 
science every day, and have been for a long time! 

Please... let me know how I can help!