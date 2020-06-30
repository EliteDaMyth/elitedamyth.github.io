---
layout: post
title: How I started a globally trending COVID tracking API during quarantine!
subtitle: Making an API is easy! You can do it too!
tags: [disease.sh, API, node, javascript]
readtime: true
image: /assets/img/disease-sh-logo.png
comments: true
---

### How Exactly did this start?
Time to go in a flashback! So the date is May 5, 2020. The coronavirus wasn't that big of a deal. There were 500 total cases in the USA, so no one really thought about it. I, at home, was quite bored. I wanted to build something (A discord bot). So I got a great idea 

> Why not make a discord bot to show how many people are affected

I immediately messaged a friend (dicedtomato) about the idea. We talked for a while, and we came to the decision that we will scrape the data from [worldometers](https://www.worldometers.info/coronavirus/). I had a tiny bit of experience scraping, so we decided that I would do the scraping part while he made the actual bot. 
Now, I started making a ridiculously easy scraper for worldometers. It was literally less than 50-60 lines. The whole API was ~ 100 lines [(But to make it look like a lot of code I added random comments and lines :P)](https://github.com/disease-sh/API/commit/93cf809ae2fa0275ba8f65ccd67e24632bcdb17b#diff-357b825e70a77bca42fdab9d1b3ee624)
At this point, the API had 2 endpoints (all, countries). The API was hosted on [https://glitch.com/](https://glitch.com/) on the free plan because I never thought it would get more than 5000 requests/hour *remember: this API was made just for using in the bot* 
The bot was almost done at this point and connected with the API, and stuff was wired up and working nicely. ![GIF of working bot](https://s5.gifyu.com/images/9sjnPibcgc.gif)
This is how the bot looked like.

Now that the bot was done, I started advertising it all over the place (Big Reddit subs), and in no time, the bot started gaining ALOT of servers. As far as I remember, we reached almost 2 THOUSAND servers the first day, and my Reddit posts got like 4k upvotes.

As the bot gained servers, people started asking me where the data was fetched from. At this point of time, I thought *The API **could** be useful for some people who wanna make a discord bot or some shit*, So I pointed the subdomain [corona.lmao.ninja](https://corona.lmao.ninja) *(This was clearly not meant for people to use)* to my glitch project. I gave the link to some of my friends. Now, Everything was going great, The bot was growing fast as fuck, and that's all I cared about. After 2-3 days, our API frequently hit the 5k requests/hour mark. We thought it was probably because of the bot, so we moved to AWS free plan. I also made a half-line API wrapper for the API 

```javascript
for(const o of["all","countries"])exports[o]=(async()=>{const t=await require("node-fetch")(`https://corona.lmao.ninja/${o}`);return await t.json()});
```

Yes, This was the actual API wrapper. *IKR I have IQ 6969*

Now after a few days, We started getting even more issues. My AWS instance frequently restarted and stuff. I thought it was just because of the free plan. I had absolutely no idea about how many people were actually using the API (I didn't really look at Cloudflare analytics). Because of AWS problems, We moved to a Google cloud free trial VM (4 Gigs of ram/2 cores). Everything was fine until a few more days. The bot was in almost 15-20k servers. It was getting harder and harder to manage every day. At this point, my partner had given up on the bot. It had quite a lot of bugs, and he was quite stressed. Now I did not know what was going on with the API. I decided to open Cloudflare analytics. I go to domain lmao.ninja, and I see the number of requests. WHAT THE FUCK 1 MILLION REQUESTS IN A WEEK. So apparently, the API was getting popular. I went to my google search dashboard, and the API got almost 1000 clicks from google search. Postman also added it to their [COVID-19 API Resource Center](https://covid-19-apis.postman.com/). The API homepage redirected to the GitHub project. I usually don't open Github frequently, so when I saw the repo, I was surprised. We had gotten 500 STARS! I did not even know about this. We had a couple of open PR's and issues. I had never managed such a big project before. I was overwhelmed by the traction it gained. 

### The ting goes brrrrrr.

Yes, so now, I started going through the issues and pull requests. I couldn't understand why people would waste their precious time to make issues and write code for something they don't get paid for and/or doesn't benefit them. Slowly and gradually, the codebase started expanding. From a 100 line file, it grew to 5-10 thousand lines! A lot of people began contributing directly or indirectly. People began suggesting more sources, governmental data, and all kinds of new features.
The API didn't have stable hosting at this point too. So `ravy` Offered to host it on her dedicated server. This was obviously an opportunity where I couldn't say no. She was already running an instance of our API on api.caw.sh (Cause of our shitty downtime), so we pointed the domain corona.lmao.ninja to her server and voila! We, Now, Get almost 150-200 Million requests each day throughout our 3 domains (disease.sh, corona.lmao.ninja, api.caw.sh)! The project was also trending on GitHub for more than a week!

### How did corona.lmao.ninja become disease.sh
One day, while talking about the API we randomly had the thoughts of *What will we do after the pandemic is over?* ravy had a great idea. Rebrand to disease.sh!

And that is how corona.lmao.ninja became disease.sh.

### Future of the API
We have decided that we will be adding some more diseases along with our V3 release (Scheduled for July 1, 2020). The API is here to stay for a while, and we have no plans of closing down as the COVID-19 pandemic ends (Which I don't see happening soon either). We are also working with a company to make the API more accessible to everyone! (More on this soon!)

### Tips for expanding your own API

 1. Make the API unique. Making an API for something for which another API exists already is pointless
 2. If something is new, Make an API for it. The early bird catches the worm.
 3. Advertise in different places. (For example, Reddit really helped.)
 4. Think about simplicity without compromising features. People will choose APIs which have more features and easier to use.
 5. **Make it open-sourced** I cannot stress this point enough. Making your API open source will make your life a lot easier. Even if you don't think anyone would contribute, there are still people who will.

### Important People
- **Ethan** - At the moment of writing this, more than half the code in our GitHub repo is written by Ethan! 
- **Julian** - Just like Ethan, He has helped a lot writing code. if the code in the repo is not written by Ethan, It's probably Julian who has written it.
 - **Ravy** - She has helped a lot with the API. If it was not for her, this API would probably not be as big as it is today!
 - **Myself** - Obviously, I am the coolest of the team who does all the work :P (PS This is sarcastic, I literally don't do anything.)

### Last Words
Just go for it.

If you wanna talk, Add me on discord: EliteDaMyth#0690.

kthxbye
