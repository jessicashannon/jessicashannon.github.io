---
layout: post
title: Chrome Extensions for Not Getting Fired
---

Small problem: our development, staging, and production environments look EXACTLY ALIKE.

I'm not saying I would ever be so silly as to mix them up.  But it wouldn't be great if I did.  Imagine if I were trying to implement a soft delete for our users and went testing it in production thinking it was local? Hahahaha.  Craziness.  Who would do that?  ANYWAY.

I learned all about using vi, grep, and sed to search through server logs.  Also, how to access an AWS snapshot with PGAdmin.  But the most valuable lesson I learned was never to mix up my browser tabs ever again!  So I wrote a quick Chrome Extension to help.

Chrome Extensions seem intimidating, but they're just that: extensions of your page.  You can get one up and running in minutes.

I started with [this tutorial](https://robots.thoughtbot.com/how-to-make-a-chrome-extension), which walks you through the basics of making an example Chrome Extension.  

*manifest.json*:

    {
      "manifest_version": 2,
      "name": "Job Saver",
      "version": "0.1",
      "content_scripts": [
      {
        "matches": ["http://mycompanysiteurl.com/*", "http://otherurl.com/*"]
        ,
        "js": ["jquery-2.1.4.min.js", "content.js"]
      }
    ]
    }

You can see I'm referencing two files: [jQuery](http://code.jquery.com/) and content.js. Loading order is important, because Javascript, so put jQuery first.

*content.js*:

    function turnRed(){
      $('.nav-main-container').css('background-color', 'red');
      };

    function turnPurple(){
      $('.nav-main-container').css('background-color', 'purple');
      };

    var url = window.location.href
    function colorChoice(){
      if ( url.search("staging") != -1 ){ turnPurple(); }
      else { turnRed(); };
    };

    colorChoice();

They suggest you use jQuery to pull the first external link off the page, and open it in a new tab.  I have plenty of tabs open already, thanks!  So instead I pick a DOM element by its CSS selector (the header) and change its color with a simple conditional.

Now staging is purple, production is red, and I still have a job. Amen.

[Github repo here.](https://github.com/jessicashannon/thrive-dev-chrome-extension/blob/master/content.js)
