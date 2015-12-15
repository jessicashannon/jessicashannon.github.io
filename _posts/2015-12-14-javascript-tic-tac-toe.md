---
layout: post
title: javascript tic-tac-toe
---

## so, I have a job now ...

And we use React.js as well as Ruby.  With Coffeescript, no less!

I did "learn" Javascript in school, but we tore through it so fast that it went in one ear and out the other, pausing in the middle just long enough for me to finish my labs.  Then I made it worse by only writing Ruby after school.  I forgot so much Javascript that when I'd watch tutorials it didn't make sense.

But I have to work on React content, and for that I need Coffeescript, and for that I need to remember my Javascript.

I decided to go back to the basics.  I'd rebuild the tic-tac-toe game I wrote in Ruby for my Flatiron application, but this time in Javascript.

<img src="public/js-ttt.png">

If your heart has ever desired a 1x1 or 8x8 tic-tac-toe game, I made it happen.  You can play it [here](http://rosieonrails.com/games).

The first night I could barely remember any syntax.  Ouch.  But the next day it all came back, and I was flying along.  

One feature I really wanted before school, but didn't know how to implement, was dynamic board sizing.  Here the board and the win conditions are created dynamically in Javascript.

Assigning a click function to each button in the set, and to each square in the board, was made ridiculously simple by Javascript's "this".  Assuming that the jQuery variable $square is the set of all my squares:

    $square.click(this, takeTurn);

jQuery iterates over them and copies the function to each.  It's beautiful.

Abstracting the win logic was not bad, but getting the board to re-render gave me trouble.  When I clicked the button to generate the board it only flashed for a split second.  Even the error messages disappeared.  This is because the button click triggers a page reload, or something like it.  And then the click event also *bubbles*, or *propogates*, traveling upward through the parent elements.  Here's how to disable it:

    function(e){
      e.preventDefault;                 // you may only need one
      e.stopPropogation;                // and not both of these - try it out
    };

    function(){                         // or use 'return false' instead!
      return false;                     // less clear, but looks nicer
    }

I also had to reassign my selector for the squares and, surprisingly, reattach the click event to get it to work.  

    function setBoardSize(){                              
      boardSize = parseInt($(this).text().split("")[0]);  
      renderTableHTML(boardSize);
      $square = $(".square");
      $square.click(this, takeTurn);
      return false;
    };

A fun weekend project!

It's not sophisticated code. My variables are all declared in the global namespace.  It's not object-oriented.  My HTML is all up in my Javascript.  Frankly, it's a mess.  But it works and you can play it!

Best of all, I now remember enough Javascript to engage with the books I bought about Javascript that will remind me how to write better Javascript.
