---
title: Understanding User Agents
author: Jacob Rozran
date: '2015-06-19'
slug: understanding-user-agents
categories: [User Agents]
tags: [learning, user agents]
---

### INTRODUCTION

I have had a few discussions around web user agents at work recently. It turns out that they are not straightforward at all. In other words, trying to report browser usage to our Business Unit required a nontrivial translation. The more I dug in, the more I learned. I had some challenges finding the information, so I thought it be useful to document my findings and centralizing the sites I used to figure all this out.

Just a quick background: Our web application, for a multitude of reasons, sends Internet Explorer users into a kind of compatibility mode in which it appears the browser is another version of IE (frequently 7, which no one uses anymore). In addition to this, in some of the application logs, there are user agents that appear with the prefix from the app followed by the browser as it understands it - also frequently IE7. For other browsers - it could be Google Crome (GC43; 43 is the browser version) or Mozilla Firefox (FF38; same deal here with the version number) - it does the same thing, though those browsers do not default to a compatibility mode in the same way.

This is only the beginning of the confusion that is a web user agent string.

While there isn't much I can do about the application logs doing its own user agent translations (we'll need to make some changes to the system logging), I can decipher the users strings from the places in the app that report the raw user agent strings. These are the strings that begin with Mozilla (more on that below). Let's walk through them.

### THE USER AGENT STRING

It can look like many different things. Here are some examples:

* Mozilla/5.0 (Windows NT 6.1;; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.81 Safari/537.36  
* Mozilla/5.0 (Windows NT 6.3;; WOW64;; rv:31.0) Gecko/20100101 Firefox/31.0  
* Mozilla/5.0 (Macintosh;; Intel Mac OS X 10_10_3) AppleWebKit/600.5.17 (KHTML, like Gecko) Version/8.0.5 Safari/600.5.17  
* Mozilla/5.0 (compatible;; MSIE 9.0;; Windows NT 6.1;; WOW64;; Trident/7.0;; SLCC2;; .NET CLR 2.0.50727;; .NET CLR 3.5.30729;; .NET CLR 3.0.30729;; Media Center PC 6.0;; .NET4.0C;; .NET4.0E)  
* Mozilla/4.0 (compatible;; MSIE 7.0;; Windows NT 6.1;; WOW64;; Trident/7.0;; SLCC2;; .NET CLR 2.0.50727;; .NET CLR 3.5.30729;; .NET CLR 3.0.30729;; Media Center PC 6.0;; MAEM;; .NET4.0C;; InfoPath.1)  
* Mozilla/4.0 (compatible;; MSIE 8.0;; Windows NT 5.1;; Trident/4.0;; .NET CLR 1.0.3705;; .NET CLR 1.1.4322;; Media Center PC 4.0;; .NET CLR 2.0.50727;; .NET CLR 3.0.4506.2152;; .NET CLR 3.5.30729;; InfoPath.3;; .NET4.0C;; yie8)  
* Mozilla/5.0 (compatible;; MSIE 9.0;; Windows NT 6.1;; Trident/5.0)  

As you can see - they all have different components and parts to them. Some seem to be very straightforward at first glance (keyword: seem) and others are totally baffling.

### TRANSLATING THE USER AGENT STRING

Much of my understanding of these user agent strings came from plugging the user agent strings into this page and a fair amount of Googling.

Let's pull apart the first user agent string from above: Mozilla/5.0 (Windows NT 6.1;; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.81 Safari/537.36

* Mozilla/5.0  
  + "MozillaProductSlice. Claims to be a Mozilla based user agent, which is only true for Gecko browsers like Firefox and Netscape. For all other user agents it means 'Mozilla-compatible'. In modern browsers, this is only used for historical reasons. It has no real meaning anymore"  
  + **TRANSLATION** We don't care about this field in any of the user agent strings. It's good to know that it starts the web user agent strings, but that's about it.  
* (Windows NT 6.1;; WOW64)  
  + Operating System = Windows 7  
  + **TRANSLATION** This is at least in the right ball park, but still not exactly straightforward. Why can't it just be Windows 7 for Windows 7?  
* AppleWebKit/537.36  
  + "The Web Kit provides a set of core classes to display web content in windows"  
  + **TRANSLATION** I don't even know... don't care.  
* (KHTML,  
  + "Open Source HTML layout engine developed by the KDE project"  
  + **TRANSLATION** Still don't know or care.  
* like Gecko)  
  + "like Gecko..."  
  + **TRANSLATION** What? Yep. Don't care - makes no sense.  
* Chrome/43.0.2357.81  
  + This is the browser and it's version  
  + **TRANSLATION** Google Chrome v. 43. YES! ONE THAT MAKES SENSE AND HAS INFO WE WANT!  
* Safari/537.36  
  + "Based on Safari"  
  + **TRANSLATION** Um... ok? So this isn't actually Apple Safari? NOPE! It's Chrome, which makes pulling Safari quite the challenge. I'll spell that out in more detail in outlining the if statement below.
Out of that whole thing, we have several things that aren't important and several things that look like they could be another thing, but aren't.  

So... Long story short - all of that info boils down to the user coming to our site using Google Crome 43 from a Window's 7 machine.

### THE INTERNET EXPLORER USER AGENT

Confused yet? Hold on to your butts. The Internet Explorer User Agent String is the level 2 version of the previous string.

Let's look at: Mozilla/5.0 (compatible;; MSIE 9.0;; Windows NT 6.1;; WOW64;; Trident/7.0;; SLCC2;; .NET CLR 2.0.50727;; .NET CLR 3.5.30729;; .NET CLR 3.0.30729;; Media Center PC 6.0;; .NET4.0C;; .NET4.0E)

I found some light reading to explain some of what we are about to dive into.

Most important from that page is this line:

"When the F12 developer tools are used to change the browser mode of Internet Explorer, the version token of the user-agent string is modified to appear so that the browser appears to be an earlier version. **This is done to allow browser specific content to be served to Internet Explorer and is usually necessary only when websites have not been updated to reflect current versions of the browser.** When this happens, a Trident token is added to the user-agent string. This token includes a version number that enables you to identify the version of the browser, regardless of the current browser mode."

**TRANSLATION** Though the browser version above looks like MSIE 9.0 (that's clearly what the string says), the Trident version identifies the browser as actually Internet Explorer 11. I am 90% sure that our site has many many many many many customizations done to deal specifically with Internet Explorer funny business. This is why the browser appears many times as MSIE 7.0 (Like this example which is actually IE 11, too: Mozilla/4.0 (compatible;; MSIE 7.0;; Windows NT 6.1;; WOW64;; Trident/7.0;; SLCC2;; .NET CLR 2.0.50727;; .NET CLR 3.5.30729;; .NET CLR 3.0.30729;; Media Center PC 6.0;; MAEM;; .NET4.0C;; InfoPath.1))

If you'd like additional information on Trident, it can be found here.

Just to summarize: For those user agent strings from Internet Explorer, the important detail is that Trident bit for determining what browser they came from.

### PUTTING THE PIECES TOGETHER

Ok ok ok... now we at least can read the string - maybe there are a bunch of questions about a lot of this, but we can pull the browser version at this point.

After pulling all of this information together and getting a general understanding of it, I read this [brief history of user agent strings](http://webaim.org/blog/user-agent-string-history/). Now I understand why they are the way they are - though I still think it's stupid.

### DECIPHERING USER AGENTS

If you, like me, need to translate these user strings into something that normal people can understand - use this table for reference. We use Splunk to do our web scraping and analysis. By using the "BIT THAT MATTERS," I was able to build a case statement to translate the User Agent Strings into human readable analysis.

| BROWSER | USER AGENT STRING EXAMPLE | BIT THAT MATTERS |
| --------|---------------------------|------------------|
| Internet Explorer 11 | Mozilla/5.0 (compatible;; MSIE 9.0;; Windows NT 6.1;; WOW64;; Trident/7.0;; SLCC2;; .NET CLR 2.0.50727;; .NET CLR 3.5.30729;; .NET CLR 3.0.30729;; Media Center PC 6.0;; .NET4.0C;; .NET4.0E) | Trident/7.0 |  
| Internet Explorer 10 | Mozilla/4.0 (compatible;; MSIE 7.0;; Windows NT 6.2;; WOW64;; Trident/6.0;; .NET4.0E;; .NET4.0C;; .NET CLR 3.5.30729;; .NET CLR 2.0.50727;; .NET CLR 3.0.30729;; MDDCJS) | Trident/6.0 |  
| Internet Explorer 9 | Mozilla/5.0 (compatible;; MSIE 9.0;; Windows NT 6.0;; Trident/5.0;; BOIE9;;ENUSMSCOM) | Trident/5.0 |  
| Mozilla Firefox 4X.x | Mozilla/5.0 (Windows NT 6.1;; Win64;; x64;; rv:40.0) Gecko/20100101 Firefox/40.0 | Firefox/4 |  
| Mozilla Firefox 3X.x | Mozilla/5.0 (Windows NT 6.1;; rv:38.0) Gecko/20100101 Firefox/38.0 | Firefox/3 |   
| Google Chrome 4X.x | Mozilla/5.0 (Windows NT 6.0) AppleWebKit/537.36 (KHTML, like Gecko) |  Chrome/43.0.2357.81 Safari/537.36 | Chrome/4 |  
| Google Chrome 3X.x | Mozilla/5.0 (Windows NT 6.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/33.0.1750.154 Safari/537.36 | Chrome/3 |  
| Apple Safari 8.x | Mozilla/5.0 (Macintosh;; Intel Mac OS X 10_10_1) AppleWebKit/600.2.5 (KHTML, like Gecko) Version/8.0.2 Safari/600.2.5 | Version/8 |  
| Apple Safari 7.x | Mozilla/5.0 (Macintosh;; Intel Mac OS X 10_9_5) AppleWebKit/600.3.18 (KHTML, like Gecko) Version/7.1.3 Safari/537.85.12 | Version/7 |  
| Apple Safari 6.x | Mozilla/5.0 (Macintosh;; Intel Mac OS X 10_7_5) AppleWebKit/537.78.2 (KHTML, like Gecko) Version/6.1.6 Safari/537.78.2 | Version/6 |  