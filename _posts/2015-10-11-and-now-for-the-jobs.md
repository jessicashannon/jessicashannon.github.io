---
layout: post
title: and now for the jobs
---

## interviews, eep!

I'm scared, but also excited.  There are people out there who want to hire me, and I want to meet them and talk to them about all the fun code they might let me touch!

At this stage, every time I pair program with someone experienced I learn something downright revelatory.  So at worst, I get to meet a bunch of programmers, see them work, and ask them about how and why they think.  That's not bad, right?

Everyone in my class is nervous.  Which is pretty normal when no one's worked for three months and never before in tech.  But I have a lot of faith compared to how I felt came in.  Sure, I'm not fully cooked as a developer, and that's OK.  

All through Flatiron I've been stockpiling book recommendations but of course I had no time to read them.  So I'm looking forward to unemployment, for at least the first weeks.  Finally time to read all my Ruby books, listen to Railscasts, and dive into personal projects with the depth and enthusiasm they deserve.

Maybe I'll even go out dancing.

## programming is easy, people are hard

Yeah ... everything I said in my last post, ignore.  Well, not everything.  But I did a lot of learning about ActiveRecord in my last group project and had time to reflect on beginner mistakes.

Our group spent days designing and re-designing the database.  It was brutal (for me).  I'm very much a "build it fast and start debugging" person, who won't buy furniture or paint the walls until I've lived in a space for a couple weeks: I appreciate planning but I also NEED experience. And this is how I rock with my databases when I start something big.  Migrations are free!  

While I reflected at length on the role of project managers, I realized I was also persisting things in my own project's database that didn't need to be there.  Often we're so excited to wrap concepts in objects that we bog ourselves down.  Now my database is much simpler.

I'm still struggling with the matching algorithm.  I've iterated, shuffled, and rotated my arrays inside-out.  I can get a match for the most stringent situation I can think of ... but what I really want is a program that will tell me with certainty if there isn't one.

I do feel great that I was able to help another classmate with a similar problem.  When she implemented my suggestion for her sorting method she was able to change 150+ lines of code to just 12.  My problem is different enough I can't take my own advice.  But, there's hope!

## and a fun deploying-to-heroku tip

My migrations run fine on SQLite3, so when I want to reset the database, I usually just

  $ db:drop
  $ db:migrate
  $ db:seed

with impunity.

This did NOT work on Heroku.  Postgres was cranky about the order in which I deleted the tables I was phasing out.  (Delete the join table first.  So you know.)  If this happens to you, don't despair and definitely don't try to edit your migrations -- that leads to more despair.

  $ heroku run rake db:schema:load

It's faster too.
