---
layout: post
title: "Getting started with ClojureScript"
date: 2013-11-21 19:31
comments: true
categories: [programming ClojureScript]
---

I recently attended [Clojure Conj][] and had a wonderful time. I've been doing
things in Clojure whenever I can find a good fit for it, but at the conference
I was inspired to take a look at ClojureScript when I saw [MarcoPolo][]'s
[Transcience][] game which was written in ClojureScript.

  [Clojure Conj]: http://clojure-conj.org/
  [MarcoPolo]: http://github.com/MarcoPolo
  [Transcience]: http://github.com/MarcoPolo/Transcience


I sat down last night with aspirations to dig in and get something started
(likely a game for the [Github Gameoff][]) but quickly realized that
ClojureScript development didn't flow quite as smoothly as Clojure development.
My impression so far has been that this is mostly due to the short time
ClojureScript has been in the wild. With that said, I wanted to outline my
first steps, where I went wrong, and specifically: how to get a browser
attached ClojureScript repl going.

  [Github Gameoff]: https://github.com/blog/1674-github-game-off-ii

### Getting Started ###

I'm going to assume that you already have lein installed. If not, the
installation is very simple and can be found on the [leiningen][] github page.

  [leiningen]: http://github.com/technomancy/leiningen

The first step, as always, is to create a new project.

`lein new try-cljs`

We next need to edit our project.clj file to pull in ClojureScript. This can be
done by adding `[org.clojure/ClojureScript "0.0.2030"]` to the `:dependencies`
vector. We will also want the [lein-cljsbuild][] plugin. Add a `:plugin`
keyword with `[[lein-cljsbuild "1.0.0"]]` as the value to accomplish this.

  [lein-cljsbuild]: https://github.com/emezeske/lein-cljsbuild

The lein-cljsbuild plugin is configured via the `:cljsbuild` key, taking a map
as the value. We'll use something similar to what's found in the [simple example
project][] of the lein-cljsbuild github repo. It looks something like:

    :builds [{:source-paths ["src-cljs"]
              :compiler {:output-to "js/main.js"
                         :output-dir "out"
                         :pretty-print true}}]}

  [simple example project]: https://github.com/emezeske/lein-cljsbuild/blob/1.0.0/example-projects/simple/project.clj

At this point your project.clj contents should look like:

``` clj project.clj
(defproject try-cljs "0.1.0-SNAPSHOT"
  :description "FIXME: write description"
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.5.1"]
                 [org.clojure/clojurescript "0.0-2030"]]
  :plugins [[lein-cljsbuild "1.0.0"]]
  :cljsbuild {:builds [{:source-paths ["src-cljs"]
                        :compiler {:output-to "js/main.js"
                                   :output-dir "out"
                                   :pretty-print true}}]})
```

Now run `lein deps` to pull these dependencies. Once that has finished, it's
time to write some ClojureScript! Since we have specified in our project.clj
that our cljs src is in `src-cljs`, we must make this directory. `mkdir -p
src-cljs/try-cljs/`. Now, using your favorite editor, let's create
`hello.cljs` in this new directory.

Add this to the contents of the file:

``` clj hello.cljs
(ns try-cljs.hello)

(js/alert "Hello World!")
```

Save that, and run the `lein cljsbuild once` which will compile this file,
placing the output into `js/main.js` and `out/`. This is nice, but now we need
an html file to get this going in a browser. Create a file in the root of your
directory `hello.html`:

``` html hello.html
<html>
<head>
</head>
    <body>
        <script src="js/main.js" type="text/javascript"></script>
        <script type="text/javascript">goog.require("try_cljs.hello");</script>
    </body>
</html>
```

Now, you should be able to open this page in your browser. When you do you
should see the javascript alert pop up with "Hello World!" as the message.

### That was fun, but... ###

So, now we have some ClojureScript compiling to javascript and running, but
we're missing an important piece of our tool chain that makes Clojure a joy to
work with: the REPL. Let's get that up and running next.

There are a few ways to get a repl running, for this post we will use the repl-listen
option provided by lein-cljsbuild. First we must modify our hello.cljs file to
look like:

``` clj hello.cljs
(ns try-cljs.hello
  (:require [clojure.browser.repl :as repl]))

(repl/connect "http://localhost:9000/repl")

(js/alert "Hello World!")
```

Save and run `lein trampoline cljsbuild auto`. This differs from the `lein
cljsbuild once` in that we are only keeping the java instance that lein
requires long enough to get our clojure process in proper order and for
cljsbuild to monitor the cljs files for changes and auto compile them when they
change. This is particuarly useful as we do not have to wait for the JVM to
fire up everytime we want to compile, but at the price that a JVM instance
stays alive until we kill the process.

Next, run `lein trampoline cljsbuild repl-listen`. This will fire up
a ClojureScript REPL and you should see:

    Running ClojureScript REPL, listening on port 9000.
    To quit, type: :cljs/quit
    ClojureScript:cljs.user>

Now, it's time to try out our page again. Instead of opening `hello.html`
directly, navigate your browser to `http://localhost:9000/hello.html`. You should now see
the same javascript alert from earlier. Now, in the ClojureScript REPL, we can
interact with the page we just navigated to. Run `(js/alert "The REPL works")`
from the REPL. The message should appear as we would expect. 

### All your browsers are belong to us? ###

That is culmination of the knowledge I gained while working through the
documentation for getting a ClojureScript REPL running in the browser.
I particuarly struggled with connecting to the REPL as it was not immediately
obvious how the connection was made. Google ended up not being much help, until
I found this [google group thread][]. I discovered that all I needed to do was
navigate to the `http://localhost:9000/`, not `http://localhost:9000/repl`.
I was also using index.html instead of hello.html last night, hopefully this
distinction is helpful in the URI's as I did not realize that port 9000 was
serving pages from the root of my project. 

  [google group thread]: https://groups.google.com/forum/#!msg/clojure/BQa9WkRvloo/tyMnl0eWKFMJ

I'm excited to experiment more with Clojure and ClojureScript. I'm likely going
to give cemerick's [Austin][] a go next. I've created a github repository
[here][] that contains the complete code written in this post, so if you don't
want to type it all out, go ahead and clone it!

  [Austin]: https://github.com/cemerick/austin
  [here]: https://github.com/jprof/cljs-browser-repl-tutorial


