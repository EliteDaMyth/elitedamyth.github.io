---
layout: post
title: How I Faked Millions of NPM Downloads!
subtitle: Faking NPM downloads is the easiest thing to do!
tags: [npm, hacking]
readtime: true
---

### A bit of backstory.
Ok, so this is my first ever blog post. I am somewhat nervous about writing this. A few months back, I built a [useless NPM package](https://www.npmjs.com/package/getanimals) to get random animal images. This was a wrapper made just for personal use. The API, which this was based on, basically re-served the images from different APIs. So one day, I stumbled upon [this article by npm](https://blog.npmjs.org/post/92574016600/numeric-precision-matters-how-npm-download-counts). So basically what that article says is 
> they (package downloads) are simply a count of the number of HTTP 200 responses we served that were tarball files, i.e., packages.

When I read that line, something clicked my mind. Did this mean I could repeatedly fetch the tarball of my package and increase the download count?!?!?!?
Apparently, Yes.
### Pre-Requisites

 1. Node JS
 2. A package on NPM

### Steps
 1. Get the URL of the tarball of your package. How? Go to [https://registry.npmjs.org/packagename](https://registry.npmjs.org/) (In my case [https://registry.npmjs.org/getanimals](https://registry.npmjs.org/getanimals)), 
 Then search for "tarball": and get a link which looks like `"tarball": "https://registry.npmjs.org/packagename/-/packagename-1.0.1(actual version).tgz"`
 2. Now half the work is done. You have to make a simple script to fetch that URL (https://registry.npmjs.org/getanimals/-/getanimals-1.0.1.tgz) repeatedly.
 To do this you can use a simple package like axios and use the `setTimeout() `function in JavaScript
 ```js
const axios = require('axios');
setTimeout(addDL, 1000);

function addDL() {
    var a = 0;
    axios.get('https://registry.npmjs.org/getanimals/-/getanimals-1.0.1.tgz').then(response => {
        a++
        console.log(`Added ${a} Downloads.\n`);
    });
}
 ```
 So basically, what this code does is fetch the tarball of your package every 1000 milliseconds (1 second.)
 
3. Profit????

### Last words.
I do not recommend you do this as this is a dick thing to do, and this can potentially strain NPM servers! If you want to talk about this, then add me on discord! EliteDaMyth#0690.
PEACE!
