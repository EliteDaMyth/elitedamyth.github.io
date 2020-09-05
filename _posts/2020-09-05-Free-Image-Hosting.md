---
layout: post
title: Make your own image sharing domain using cloudflare workers and imgur!
subtitle: Cloudflare Workers are Amazing! Make your own Image Hosting with cloudflare and imgur!
tags: [cloudflare, image, free hosting, imgur]
readtime: true
image: https://miro.medium.com/max/392/1*6bqgBkbNo7kXLv2qXU6NHQ.jpeg
comments: true
---

### How does it work?
So what we are going to do, is to upload our images to imgur, then use our own domain as a "Proxy" for the imgur images. We will be using Cloudflare workers to do this as it is free and easy to setup!
A hosted example can be found at [cdn.elitedamyth.xyz](https://cdn.elitedamyth.xyz/)
so basically, the url [https://cdn.elitedamyth.xyz/q7LwAVB.png](https://cdn.elitedamyth.xyz/q7LwAVB.png) is a proxy for [https://i.imgur.com/q7LwAVB.png](https://i.imgur.com/q7LwAVB.png)! I will be using sharex as it is a free and open-sourced tool.


### Requirements:

 1. A domain 
 2. [Cloudflare](https://cloudflare.com) account
 3. [ShareX](https://getsharex.com/) installed
 4. Imgur account (Optional)

### Setting up cloudflare workers:

 - Add your domain to cloudflare, wait for the DNS changes to propagate. 
 ![Add Site](https://cdn.elitedamyth.xyz/0TwI5Pu.png)

 - Go to cloudflare workers
 ![Workers](https://cdn.elitedamyth.xyz/Xq0otVD.png)

 - Make a new worker with any name. Use this code but make sure to edit the `DOMAIN` variable:
<script src="https://gist.github.com/EliteDaMyth/b5cc4565a0af197d9a6962eff0226e12.js"></script> 
[Gist](https://gist.github.com/EliteDaMyth/b5cc4565a0af197d9a6962eff0226e12) 
 ![Worker](https://cdn.elitedamyth.xyz/dlVvSkz.png)
 - Turn on the worker, Now go to your domain, then the Workers tab: 
 ![Worker Tab](https://cdn.elitedamyth.xyz/CeuxZ7i.png)
 - Click on Add Route, Then enter `subdomain.yourdomain.tld/*` and select the worker you have created earlier. 
 ![tld](https://cdn.elitedamyth.xyz/oOgotIP.png)
 - Make an A record for the subdomain you chose earlier, that points to 192.0.2.1 or any other IP address. Make sure the record is proxied through cloudflare.
 ![record](https://cdn.elitedamyth.xyz/vZvCFHv.png)
 - You are done setting up the worker part! Now all that is left is changing your sharex settings.

### Setting up Sharex:
 - Set your image uploading destination to Imgur. 
 ![imgur](https://cdn.elitedamyth.xyz/5RS9T6v.png)
 - Click on "After Upload Tasks" and select Shorten URL.
 ![Shorten URL](https://cdn.elitedamyth.xyz/FhLRFo9.png)
 - Go To Destinations > Custom uploader settings and Import from clipboard;
  ```js
  {
   "Version": "12.4.1",
   "Name": "imgur domain change",
   "DestinationType": "URLShortener",
   "RequestMethod": "POST",
   "RequestURL": "https://cdn.elitedamyth.xyz",
   "Body": "JSON",
   "Data": "{\"url\":\"$input$\"}",
   "URL": "$response$"
 }
 ```
 ![image](https://cdn.elitedamyth.xyz/NkyMwtx.png)
 - Change the URL to your own domain and save.
 - Go to Destinations -> URL Shortener -> Select Custom URL shortener
 ![shortener](https://cdn.elitedamyth.xyz/YWvraGF.png)

 - That's it! You have a fully working and free Image hosting domain! 
 Add me on discord if you encounter any issues (EliteDaMyth#0690)
