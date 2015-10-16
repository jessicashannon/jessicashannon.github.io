---
layout: post
title: No Code Left Behind
---

Today is graduation day!  Which means: soon, I have to give back the shiny MacBook Air I borrowed for school.  I have more than a hundred repos and many of my unfinished labs aren't committed.

So I found and modified a bash script that will find repos, stage and commit the changes, and push them to Github!

To run it, give it executable permissions:

    // ♥ chmod +x .gitcheck

Then call it via relative path.

    // ♥ ../../.gitcheck  # since my repos live in /Development/code

Here's the gist:

<script src="https://gist.github.com/jessicashannon/0a54c25c2c73889ead73.js"></script>

[Original script](https://astrofloyd.wordpress.com/2013/02/10/gitcheck-check-all-your-git-repositories-for-changes/), with thanks.
