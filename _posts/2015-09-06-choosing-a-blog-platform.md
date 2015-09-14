---
layout: post
title: Choosing a Blog Platform
---

When I launched this blog, it was on Octopress and it was a hot mess.  Nothing against Octopress, but if you aren't good with git, things can go wrong fast!

Since I planned to reinstall it, I had the chance to look at other blogging platforms.  My initial thought was to use (or build!) a Rails-based platform and host it on Heroku, but after reading a little I decided it was overkill.

The idea behind static site generators like Octopress -- which I did not understand when I first installed it -- is to give you the benefits of a dynamically served website, without its downsides.  With a dynamic website you write one small piece (say, the text) and your site assembles a finished project around it for the user: styling, partials, links, paths, the works.  This is what Wordpress does.  Wordpress runs on MySQL and you have to manually create a database during the installation.  

But if 300 people view your Wordpress site at once, it will probably break.  You're generating it each and every time someone hits the site.  Popular websites that run on Wordpress employ caching, which is interesting, but beyond the scope of this post.

Octopress does this generation only once, when you publish a post.  The static page it creates is served to your viewers.  Then if 300 people view your site simultaneously, you can start worrying about your bandwidth.

Octopress is based on Jekyll, but personally, I picked Jekyll itself because it seems more widely used.  I figured it would have better themes and I'd have better luck solving problems when it broke.  Also, you can't break Jekyll by pushing to the master branch.

Jekyll comes without so much as a theme.  [Try these](http://jekyllthemes.org/)!  If you're installing Jekyll after Octopress, check out [jekyll-compose](https://github.com/jekyll/jekyll-compose), which gives you the automatic post generation you know and love.

If you need to understand every line of code, consider a tiny platform like [Toto](https://github.com/cloudhead/toto) ("a git-powered, minimalist blog engine for the hackers of Oz").  It runs on Rack and tops out at about 300 lines of code!

In setting up this blog fresh, I wanted to know what made these "programmer" platforms.  Sure, you need a passing familiarity with git, but is that all?  Do programmers use something like Jekyll because it's easier and better, or is it a culture thing?  

The usual non-programmer choice is Wordpress.  But setting up Wordpress is not trivial.  There are many folders and many files, so you need FTP or SSH access to your server, and an FTP or SSH client to upload them.  There's a key you have to get from the Wordpress gods.  And there's the previously mentioned MySQL database.  If you want to customize your theme, you have to write CSS.  I did all of this as a non-programmer, but I didn't understand it.

What distinguishes Wordpress is how you write posts: with a simple GUI in the browser window after logging in, or in another graphical Wordpress client.  I hear there are lovely Wordpress apps for mobile, but I've never used them.

When you use something like Jekyll, you write markdown in a text file and put that file in a folder.  Then you use simple shell commands to build the site and use git to synch it.  You can't post via mobile unless you have a tablet with SSH access.  (Edit: I think [it may be possible to post on Jekyll with prose.io](https://developmentseed.org/blog/2012/june/25/prose-a-content-editor-for-github/)).

Wordpress sounds simpler, right?  So I installed a fresh copy to my hosting service.  Many things are difficult right now and perhaps my blog doesn't need to be one of them.

To my dismay, everything had changed.  I downloaded some plugins but none of them did what I wanted.  And I felt ... uncomfortable .... in its GUI.  I never noticed how much I disliked its design.  I don't know what half the buttons do.  I never did. And even the ones I did use (say, to embed media) seem worryingly ambiguous now. You mean I have to browse through my whole computer through Finder looking for the file and then click to upload it just kind of hoping it works?  And it saves it just wherever?  HOW IS THAT ANY WAY TO LIVE?

So it begins ...

The answer is: if you would rather type than use Finder to find an image file, copy it to your local repo via the command line, and write your blog post in markdown -- programmer blogs are for you.

Also, while I wasn't looking, I became a programmer.

I ripped Wordpress off and put Jekyll on and felt much better.
