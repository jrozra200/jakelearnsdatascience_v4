---
title: Identifying Compromised User Accounts with Logistic Regression
author: Jacob Rozran
date: '2015-09-26'
slug: identifying-compromised-user-accounts
categories:
  - Data Science
  - Statistics
tags:
  - data science
  - R
  - logistic regression
  - statistics
---

### INTRODUCTION

As a Data Analyst on Comcast's Messaging Engineering team, it is my responsibility 
to report on the platform statuses, identify irregularities, measure impact of 
changes, and identify policies to ensure that our system is used as it was 
intended. Part of the last responsibility is the identification and remediation 
of compromised user accounts.

The challenge the company faces is being able to detect account compromises 
faster and remediate them closer to the moment of detection. This post will 
focus on the methodology and process for modeling the criteria to best detect 
compromised user accounts in near real-time from **outbound email activity**.

For obvious reasons, I am only going to speak to the methodologies used; I'll be 
vague when it comes to the actual criteria we used.

### DATA COLLECTION AND CLEANING

Without getting into the finer details of email delivery, there are about 43 
terminating actions an email can take when it was sent out of our platform. A 
message can be dropped for a number of reasons. These are things like the IP or 
user being on any number block lists, triggering our spam filters, and other 
abusive behaviors. The other side of that is that the message will be delivered 
to its intended recipient.

That said, I was able to create a usage profile for all of our outbound senders 
in small chunks of time in Splunk (our machine log collection tool of choice). 
This profile gives a summary per user of how often the messages they sent hit 
each of the terminating actions described above.

In order to train my data, I matched this usage data to our current compromised 
detection lists. I created a script in python that added an additional column in 
the data. If an account was flagged as compromised with our current criteria, it 
was given a one; if not, a zero.

With the data collected, I am ready to determine the important inputs.

### DETERMINING INPUTS FOR THE MODEL

In order to determine the important variables in the data, I created a Binary 
Regression Tree in R using the rpart library. The Binary Regression Tree iterates 
over the data and "splits" it in order to group the data to get compromised 
accounts together and non-compromised accounts together. It is also a nice way 
to visualize the data.

You can see in the picture below what this looks like.

![regression_tree_for_class](/img/regression_tree_for_class.png)

Because the data is so large, I limited the data to one day chunks. I then ran 
this regression tree against each day separately. From that, I was able to 
determine that there are 6 important variables (4 of which showed up in every 
regression tree I created; the other 2 showed up in a majority of trees). You 
can determine the "important" variables by looking in the summary for the number 
of splits per variable.

### BUILDING THE MODEL

Now that I have the important variables, I created a python script to build the 
Logistic Regression Model from them. Using the statsmodels package, I was able 
to build the model. All of my input variables were highly significant.

I took the logistic regression equation with the coefficients given in the model 
back to Splunk and tested this on incoming data to see what would come out. I 
quickly found that it got many accounts that were really compromised. There were 
also some accounts being discovered that looked like brute force attacks that 
never got through - to adjust for that, I added a constraint to the model that 
the user must have done at least one terminating action that ensured they 
authenticated successfully (this rules out users coming from a ton of IPs, but 
failing authentication everytime).

With these important variables, it's time to build the Logistic Regression Model.

### CONCLUSION

First and foremost, this writeup was intended to be a very high level summary 
explaining the steps I took to get my final model. What isn't explained here is 
how many models I built that were less successful. Though this combination worked 
for me in the end, likely you'll need to iterate over the process a number of 
times to get something successful.

The new detection method for compromised accounts is an opportunity for us to 
expand our compromise detection and do it in a more real-time manner. This is 
also a foundation for future detection techniques for malicious IPs and other 
actors.

With this new method, we will be able to expand the activity types for compromise 
detection outside of outbound email activity to things like preference changes, 
password resets, changes to forwarding address, and even application activity 
outside of the email platform.