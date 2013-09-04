---
layout: post
title: "Ludum Dare 27 Post Mortem"
date: 2013-09-04 19:09
comments: true
categories: [programming, Ludum Dare, CoffeeScript]
---

This time around I've managed to get to writing this in a more timely fashion.
Ludum Dare 27 was almost two weeks ago, and so the judging is still going on
for my entry "Get to the Choppa!". Overall this Ludum Dare went much smoother
than the previous. The theme this time around was "10 Seconds" which lent
itself to the game idea I had in mind. 

The Idea
--------

Learning from the experience I had in Ludum Dare 26, I decided that having
a better defined idea for the game _before_ the theme was announced would make
the development go much smoother. I had been playing [Organ Trail][] when I had
time to kill in July and August, and I was enjoying the simplicity of the
scavenging missions. I knew that I wouldn't be devoting the full weekend to
this Ludum Dare like I had the last, so I thought aiming for gameplay similar
to this for my entry would be reasonable. I also loved the retro style of Organ
Trail, and so I wanted the game to be visually similar. 

  [Organ Trail]: http://store.steampowered.com/app/233740/

The Saturday before Ludum Dare I happened to re-watch [this awesome Predator
video][] and ["GET TO THE CHOPPA!"][] popped into my head. I knew now what the
goal of every level of my game would be: Getting to that choppa! Since
CoffeeScript and Crafty.js hadn't been a bad experience, I decided to use them
again for implementing the game. I described the idea to some of my friends and
luckily they wanted to help. When it came time for the theme to be announced it
could not have been more perfect: "10 Seconds". More like: "10 Seconds to get
to the choppa!".

  [this awesome Predator video]: http://www.youtube.com/watch?v=qlicWUDf5MM
  ["GET TO THE CHOPPA!"]: http://www.youtube.com/watch?v=-9-Te-DPbSE

Getting to the Choppa!
----------------------

We didn't get started until late in the day Saturday. I wanted to reuse any
components that we could from [MetroGnome][], however the way most were
implemented they were not easy to drop in the way I had hoped. In the end we
used this code as a reference for where to begin when we had questions with how
to do something. Specifically, I had not touched anything with sprites when we
worked on MetroGnome, so being able to see how this was implemented in
MetroGnome was awesome.

  [MetroGnome]: https://github.com/jprof/ludumdare26

Since the team working on _Get to the Choppa!_ was smaller this time around it
was much easier to divvy work out and implement features concurrently. While
I was working on loading assets and animating the sprites others were working
on enemy movement and bullets. Since we had an idea of what we wanted the game
to play like and how it should look, the art quickly came together, in fact it
was finished two or three hours after we started working.

What that went well:

  *  Graphics
  *  Having a concept before the theme was announced
  *  Gameplay
  *  Smaller team
  *  Smaller scope

What could have been better:

  *  CoffeeScript/JavaScript can resemble insanity
  *  We still need more experience with Crafty.js
  *  No sound

Overall this Ludum Dare flowed much better than the previous one. Having a
concept before the competition started was huge, as well as having a smaller
team and scope. Despite going better overall, I still found myself working on
the project up to the deadline. When I reached the point where it was time to
implement the level loader, I kept finding bugs. Part of this is due to the
dynamic nature of JavaScript. It's easy to develop something quickly with
JavaScript or CoffeeScript, but it's a pain to debug.

Despite it's flaws, I'm still happy with the outcome: [Get to the Choppa!][].

  [Get to the Choppa!]: http://jprof.github.io/ludumdare27

Next Time
---------

So, after participating in the last two Ludum Dare Game Jams, I've definitely
found that having a concept prior to the event is huge and I will most
certainly have an idea before the next one. I've used Crafty.js and
CoffeeScript for both competitions, and despite the rough spots I will likely
use them again. I would really like to take some of the pieces that we
developed for _MetroGnome_ and _Get to the Choppa!_ and work on their design so
that we can potentially reuse them in the next Ludum Dare. I also feel that
getting the level loader up earlier (this was the last piece I worked on) would
be huge. The game didn't feel like a game until the levels were loading. 

The next Ludum Dare will be sometime in December. I hope to devote more time to
it than I did for this one. 

