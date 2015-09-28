---
layout: post
title: It Takes Two to ... Match?
---

##the problem

A friend of mine, Melissa, volunteers as a swing dance conference organizer.  She works for weeks making sure needy guests and teachers are housed with volunteer hosts. She keeps a manually updated Google spreadsheet, and then matches on a slew of criteria (will they sleep on the floor? are they allergic to cats?) with pencil and paper.

It may sound crazy for folks -- often complete strangers -- to put each other up in this day and age, but between broke attendees, nomadic instructors, and cash-strapped conference organizers, her conference couldn't run without it.  It's harder in New York than anywhere else, but I love the tradition of "hosting" in social dance subculture.  Like an international couch-surfing network of jazz-loving weirdos in suspenders.

##the solution

I can't make New York apartments bigger, but what if I wrote her a program that matched guests to compatible hosts?  I'd give her forms so users could enter their *own* data. My program would run in seconds, it could be run again and again as her data changed, and it would always return the best possible solution.

Originally I imagined a Ruby script that would spit out a plain text file of matches.  But now I realize I can do better.

My biggest problem was big dreams.  What if users could log in and come back to change or check their answers, or their hosting status?  What if users could be guests sometimes, and hosts other times, and administrators besides?  What if they could be matched for different years -- or different events in different cities in the same year??  It got out of hand.

If Trello could manage a team, it can manage me.  So I made a Trello board and got to work.  First I wrote down all my dreams for the app, no matter how outlandish. (AJAX for everything!!1!) Then I picked out a few basic user stories and got to work.

##some things I learned

* ActiveRecord and I are cool.  I thought this day would never come.

* We know "has many"/"belongs to" relationships are two-sided -- if you have one, you need the other. dependent: :destroy does not need to be symmetrical.  I cried laughing when I found the bug where resetting my Matches (i.e. destroy and regenerate) got rid of all my users.  Sure, we've all *felt* that way when a Match dissolved, but life goes on.  Only put dependent: :destroy on the statement ABOUT the dependent thing, IN the class of the independent thing.

* Naming a model isn't just nice, it's functional.  If your model names make sense, their interactions make sense, and distributing your logic makes more sense.  At first my Hosts and Guests generated with a full set of potential host-guest matches, but those matches were useless as soon I changed any user.  After struggling to keep them updated (so many callbacks!), I realized hosts and guests don't really "own" their matches with each other, in any meaningful way.  We only need to consider their compatibility when I create a (housing) Arrangement: i.e., a unique collection of compatible matches.  Now my matching logic lives in the Match model, and fresh matches are generated whenever I call for a new Arrangement.

* Don't be scared of letting your database evolve. Migrations are free. You don't need to know the destination to start walking in the right direction.  I knew this site would be tough, because users in our Twitter clone only had two states (follower and following) and still looked like this:

<script src="https://gist.github.com/jessicashannon/5bd7ef8a43904080e00f.js"></script>

It's a lot.

So I just got started.  I don't have a single User class right now, but I *am* describing their behavior.

<script src="https://gist.github.com/jessicashannon/bc1938b1fd6caf0ee688.js"></script>

From here on out it's just debugging.

* Speaking of debugging: when you start with scaffolding, it's easy to expect that you can use your site to build your site.  And you can, including when you put the wrong output in your view and go crazy trying to figure out what broke.  Use the console.  Love the console.

* If you can't get Bootstrap to work for you, try searching for the classes and IDs in your project. Don't find it? Go to the Internet, child, for you are missing a theme file.

* Learning all that SQL was worth it.  Also, it's OK to draw out your tables on paper.

* Seed data is easy, fun, and useful.  We used [Faker](https://github.com/stympy/faker) on our Twitter clone.  I enjoyed giving our users names and writing a few simple lines of code that gave them random, but realistic, behavior.

<script src="https://gist.github.com/jessicashannon/186918fbecc539d87a03.js"></script>

Right now I'm using Faker to test.  When I add more capacity to the code, I make more users and I make them harder to match.  It's like the Sims except they help you fix your code.

##conclusion

It's both scary and inspiring making something I want people to use.  What's hilarious in testing (matching users to nonexistent hosts) is a disaster in deployment.  If people depend on this tool and I fuck it up, people could literally end up on the street.  (OK, we'd catch it ... but still.)  Privacy is a thing.  So is security.  I have to integrate with email.  And it has to be dead simple and foolproof or Melissa will go back to Excel spreadsheets.

NBD though, I'm going to leave here knowing how to do all these things.

See you at Ruby project night!
