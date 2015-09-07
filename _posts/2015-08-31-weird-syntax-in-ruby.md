---
layout: post
title: Weird Operators and Code Clarity in Ruby
---

## Or Equals (Conditional Assignment)

	if thing exists
		# do nothing
	else
		thing = initial value
	end

	if a
		a
	else
		a = b
	end

I was doing code review with Amanda, one of our instructors, and struggling with how to succinctly express the above code.

Maybe a ternary operator?

Here's the structure of a ternary operator: (if this statement is true) ? (do this) : (else do this)

	a ? a : a = b

It's a nice way to get a short if/else statement on one line, with no need for an end.

Or, you could even do it like this, Amanda said:

	a ||= b

It's called "or equals", and in my code it meant, "If a does not already exist, assign it to b".  Basically.

You can think of it as expanding to a = a || b.  

There are some odd side effects of this, though.  

unicorns = false
unicorns ||= rainbows
=> rainbows

Uh ... what?  We assigned a value to unicorns.  But because the value we assigned is false, it is reassigned to rainbows.

A better way to think of or-equals is in terms of boolean value.  If your first element is truthy, it will stay (yes, even if it's 0).  If it is falsey (false or nil) it will be reassigned.

Some people love the or-equals for its brevity, some people hate it because of weird edge cases and lack of clarity, and many people on the Internet would like Ruby noobs to shut up about it.

## Flip-flopping

The other weird symbol I came across is the flip-flop.

..

or

...


It looks like a range, right?  But it's not a range: it's a problem.

Let's take this paragraph from the [Bacon Lorem Ipsum](https://baconipsum.com) generator:

	bacon = "Bacon ipsum dolor amet hamburger ground round rump pancetta veniam shoulder cow esse
	eiusmod aliquip. Aute qui esse eu cow. Ipsum id leberkas ribeye t-bone cow tri-tip elit. Sed
	bresaola pastrami, dolore tempor pork pariatur salami tenderloin short loin.".split(" ")

	bacon.each do |word|
		if (word == "hamburger")..(word == "tenderloin")
			puts "  " + word
		else
			puts word
		end
	end

Output:

	Bacon
	ipsum
	dolor
	amet
	  hamburger
	  ground
	  round
	  rump
	  pancetta
	  veniam
	  shoulder
	  cow
	  esse
	  eiusmod
	  aliquip.
	  Aute
	  qui
	  esse
	  eu
	  cow.
	  Ipsum
	  id
	  leberkas
	  ribeye
	  t-bone
	  cow
	  tri-tip
	  elit.
	  Sed
	  bresaola
 	  pastrami,
	  dolore
	  tempor
	  pork
	  pariatur
	  salami
	  tenderloin
	short
	loin.

Whaaaa?

In a flip-flop, the conditional is false until the first conditional is met.  Then it remains true until the second conditional is met, at which point it becomes false again.

I can't do better than [this description](https://blog.newrelic.com/2015/02/24/weird-ruby-part-3-fun-flip-flop-phenom/): "Have you ever longed for a way to execute part of a loop part of the time? Do you also feel like if/else statements are too “clear” and “understandable” for your clever code? Then the flip-flop operator is perfect for you!"

If you really want to hurt your brain, [check out this solution to FizzBuzz using a flip-flop](https://juliansimioni.com/blog/deconstructing-fizz-buzz-with-flip-flops-in-ruby/):

	a=b=c=(1..100).each do |num|
	  print num, ?\r,
	    ("Fizz" unless (a = !a) .. (a = !a)),
	    ("Buzz" unless (b = !b) ... !((c = !c) .. (c = !c))),
	    ?\n
	end

*hides in corner, rocks back and forth crying*

My real takeaway was about code readability, and how awesome it is to see programmers uniting against deliberately obtuse code.  

I didn't code (much) before Flatiron, so I'm just starting to realize how many preconceptions I had about programming.  I had the impression that all code was written the same: code was code was code.  Except smarter people wrote more complicated (and thus better) code.  Comments were to explain to dumber programmers the smart thing you did.  

It's been a revelation to me that more difficult code isn't always better.  And while smart people can (and do) write dazzingly complex code, so can the merely dedicated.  

After the takedown of Silk Road, I read a [long form article on it](http://www.wired.com/2015/04/silk-road-1/), and the description of one of the cops stuck with me:

"He didn’t understand programming at first. But he did understand that this was the  future, so he paced himself, stuck with it, and came out the other side as a computer forensics expert..."

It's a fascinating read with a lot of layers.  But what really stuck with me wasn't Ross Ulbricht's libertarian crusade against the failed war of drugs, or his stranger-than-fiction descent into organized crime and murder.  It was that one guy's story.  Here was this college powerlifter from a tiny town, with no particular gift for computers.  And his persistence won the day.

You don't need to be able to hold eight levels of iteration in your head to succeed in programming.  If you have to think that hard about it, there's the potential for someone else to misunderstand it.  Code can't just be clever these days.  It also needs to be clear, readable, testable, and easily maintainable.

tl:dr It's all well and great to be an anti-establishment programming savant until the cops come find you from the one question you posted under your real name to Stack Overflow.  So refactor your code, don't be too clever, and don't use flip-flops.  

If you too find yourself needing to Google weird symbols, [Symbolhound](http://symbolhound.com/) is a search engine that allows you to use punctuation.

Other links:

https://allenan.com/ruby-or-equals-operator-default-booleans/

http://stackoverflow.com/questions/995593/what-does-or-equals-mean-in-ruby/14697343#14697343

http://invisibleblocks.com/2007/06/11/rubys-other-ternary-operator/
