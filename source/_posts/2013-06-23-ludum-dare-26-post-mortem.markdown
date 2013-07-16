---
layout: post
title: "Ludum Dare 26 Post Mortem"
date: 2013-06-23 10:33
comments: true
categories: [programming, Ludum Dare, CoffeeScript]
---

This is coming a bit late... it has been a while since Ludum Dare 26! I have had
a lot going on with my family and work so I'm just now getting around to writing
this.

For those of you who are not familiar with [Ludum Dare][], it is a game
development competition. It is consists of two events: an individual, two day
competition that has a strict set of rules, and a more laid-back, team-based,
three day game jam.

  [Ludum Dare]: http://www.ludumdare.com/compo/ 

We participated in the jam! Our team consisted of five programmers and one
artist.  This was our first time participating in a Ludum Dare event which made
it a fun and interesting experience. 

Before going into the minute details, here are the canonical "what went well and
what didn't go well" lists.

What went well:

  *  Graphics
  *  CoffeeScript
  *  Sharing the same workspace
  *  Github
  *  Streamlined build process

What could have been better:

  *  Gameplay
  *  CraftyJS
  *  CoffeeScript(!?)
  *  The theme
  *  Inexperienced team
  *  Bottle-necked workload

Prequel
-------

Before the competition, we decided on using JavaScript and Crafty to write the
game. CoffeeScript was later chosen over JavaScript due to it's cleaner and more
succinct syntax (thanks to a brief love affair with [Node Wars][]). With this
knowledge, I prepared a local server that each of us could push our current
build to in order to efficiently show the progress we were making.  All of
us are Vim users so we installed the awesome plugins [syntastic][] and
[vim-coffee-script][] to assist us with CoffeeScript syntax, linting, and
compiling.

  [Node Wars]: http://nodewar.com/
  [syntastic]: https://github.com/scrooloose/syntastic
  [vim-coffee-script]: https://github.com/kchmck/vim-coffee-script

The Game
--------

_Minimalism_ was the theme of this Ludum Dare. We talked through our game ideas
and landed on using sound as the core game mechanic. We eventually came up with
the idea of using a gnome as the main character. The specifics of the sound
mechanic evolved into a metronome-like beat; its' purpose was to signify when
the player could move. Thus, Metrognome was born.

In Metrognome, the beat is tied to the movement of the player. The speed of the
gnomes' movement was tied to the accuracy of hitting the directional key with
the beat. Accurate timing results in the gnome dashing quickly in that
direction. With this design in mind, the next step was coding and developing the
art.

Since most of us had never used CoffeeScript or Crafty, there was a considerable
amount of flailing involved. The vim-coffee-script plugin was useful for the
minor mistakes so we slowly made progress. A bigger problem for us was the
Crafty documentation; we often had to resort to looking through the source for
answers instead of their published docs.

Our team composition and lack of experience plus the short duration of the jam
did not work in our favor. The first two days proved difficult for more than two
of our programmers to work in parallel; our code base was not large enough for
our team. Fortunately, the third day went better in this regard; the code
base had grown large enough for each of us to have a task that would not trample
others work.

Our experience with Crafty was also an issue. Crafty is built as an [Entity
Component System][] and this was a new design paradigm for most of us. Some of
the components we wrote resembled objects from the Object Oriented school of
thought more than what an ECS component actually should use. 

Despite our struggles with Crafty and our inexperience with CoffeeScript, we
were able to finish with a semi-working game. The graphics and art style
turned out great! It can be found [here][Metrognome] and the source
[here][Metrognome-source].

  [Entity Component System]: http://roguebasin.roguelikedevelopment.org/index.php?title=Entity_Component_System
  [Metrognome-source]: https://github.com/jprof/ludumdare26
  [Metrognome]: http://jprof.github.io/ludumdare26

