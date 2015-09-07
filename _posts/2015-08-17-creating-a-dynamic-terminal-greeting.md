---
layout: post
title: Creating a Dynamic Terminal Greeting
---

What's the deal with keyboard shortcuts?

They're fast, they look cool, and I'm told they're the way Real Programmers do it.  But most importantly for me, mousing (or using the trackpad) aggravates my nascent RSI.  And I'm not ready to have programmer injuries before ever becoming a programmer.  So while I'm much more interested in learning Ruby than learning how to type better, I know that learning keyboard shortcuts (for me) is more than just looking competent: it's a long term investment in my health and career.

You can learn and practice keyboard shortcuts on shortcutfoo.com.  But why go to a website to fetch your shortcuts when you can have them brought to you?

I thought adding a script to my terminal greeting would be easy. It wasn't hard, but it was surprisingly difficult to Google.

Here's how I thought I would do it:
* collect keyboard shortcuts, put in txt file (if being good) or array of strings (if lazy)
* write simple Ruby program to return random daily shortcut
* make Ruby program file executable with chmod
* something or other about editing the $PATH
* edit .bash_profile to call on script

I can't tell you this *doesn't* work, because I'm on someone else's computer and when I opened .bash_profile like I would on my machine,

    $ atom .bash_profile

was completely empty.  I think I created it by trying to open it.

Apparently, it's not a default thing on all Macs.  I tried:

    $ atom .bashrc

but that was empty too.  Where the heck was it getting my terminal info?

A little googling suggested that I could edit a daily greeting message at a hidden file called /etc/motd.
I tried it.  It worked.

Of course I immediately tried to write Ruby in /etc/motd and declare it executable.  It didn't break my computer,
but it didn't run as code, just put out the text of my program. Welp.

Other people looking to do it [hadn't gotten the clearest or most encouraging answers:]
(http://serverfault.com/questions/459229/is-it-possible-to-put-commands-in-etc-motd)

But [this tutorial](http://parkersamp.com/2010/10/howto-creating-a-dynamic-motd-in-linux/), while oriented more toward the sysadmin side, was what I needed.

They suggest writing a bash script:

    Edit: /usr/local/bin/dynmotd
    1
    2
    3
    #!/bin/bash

    echo -e "

But if you have to declare #!/bin/bash it has to work with other languages, right?  And, I was right!

    Last login: Sun Aug 16 19:45:37 on ttys000
    Welcome, Jessica!
    Shortcut of the Day: Ctrl + E Go to the end of the line you are currently typing on
    Clunkbook-Pro:~ jrssae$

To create this output, I edited three different files from my home directory.

    $ cd ~

The first was the static message.  Here's how to fetch it with atom (or use your text editor of choice):

    atom /etc/motd

It's a private file and you may need to access it as a superuser (add "sudo" in front).  It will prompt for your system password.

You can leave this file blank, or add a message.  Whatever is in here will stay the same and print before your
dynamic message.

Next, edit the file that's going to hold your dynamic message:

atom /usr/local/bin/dynmotd

Write your program in there. Here's mine:

    #!/usr/bin/env ruby

    terminal_shortcuts = ["Ctrl + A	Go to the beginning of the line you are currently typing on",
    "Ctrl + E Go to the end of the line you are currently typing on",
    "Ctrl + L Clears the screen",
    "Ctrl + U Clears the line before the cursor position. If you are at the end of the line, clears the entire line.",
    "Ctrl + H Same as backspace",
    "Ctrl + R Lets you search through previously used commands",
    "Ctrl + C Kill whatever you are running",
    "Ctrl + D Exit the current shell",
    "Ctrl + W Delete the word before the cursor",
    "Ctrl + K Clear the line after the cursor",
    "Ctrl + T Swap the last two characters before the cursor",
    "Esc + T Swap the last two words before the cursor"]

    puts "Shortcut of the Day: #{terminal_shortcuts.sample}"

As you can see, I took the lazy route.  Edit it however you like.  Quotes instead of keyboard shortcuts?

Next, open /etc/profile:

atom /etc/profile

Mine had stuff already in it, which was kind of a relief.  I pasted the path of my dynmotd file at the bottom.

    # System-wide .profile for sh(1)

    if [ -x /usr/libexec/path_helper ]; then
    	eval `/usr/libexec/path_helper -s`
    fi

    if [ "${BASH-no}" != "no" ]; then
    	[ -r /etc/bashrc ] && . /etc/bashrc
    fi

    /usr/local/bin/dynmotd # path goes here

I still have to get it working on my school computer, but I hope this helps someone else with the same question
about dynamic greeting messages in the terminal.  It's quick and easy and has a lot of potential for fun.
