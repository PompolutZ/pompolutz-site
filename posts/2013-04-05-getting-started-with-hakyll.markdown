---
title: Getting started with Hakyll 
---

#Introduction

One day you decided, like I did, to create your personal page with/or without blog. There are plenty of ways to do this, depending on your personal programming experience, level of lazyness and geekness. But I guess that making your personal page just to show off yourself don\'t require buying hosting and domain to create complex and mature website. So the most simple way to reach mentioned goal is to create a static website. Because:

> Static sites are fast, secure, easy to deploy, and manageable using version control.

I think there are no need to proof those reasons because they are rather clear.

That very day I came up with a decision to create my personal page, I discovered that it is possible to make one on github. You can manage deployment via \'git push -u origin master\', so it should be easy. But first you have to find some static site builder, because it will help you a lot to create everythin once, push, and then just time to time add your posts, projects or any other informaion. The most popular static site builder (SSB) Gekyll appeared to be a problem on my Windows based machines, so I\'ve found a list of alternatives where I discovered [Hakyll][1]. Because for a long time I wanted to find good way to start using Haskell for something I decided to give it a shot. And this is story how you can go by my steps :)

#Step 1. Setup
Good way to start will be downloading [Haskell Platform](http://www.haskell.org/platform/windows.html). After installation you will receive:

- [Glasgow Haskell Compiler][2] - one of the most popular ones I guess.
- GHC interactive environment - both in console mode and wrapped in a WinGHC application.
- [Cabal][3] - package manager for Haskell (Sorry, but from my point of view this is just a package manager, even though I heard somewhere that it\'s actually not)

I guess if you never have experience with Haskell before, you shold definitely try to run \'ghci\' and try out some Haskell coding. You can also could try it [online](http://tryhaskell.org/).
If you want to learn Haskell more, which is really good, you can try an AWESOME book [Learn you a Haskell for a Great Good](http://learnyouahaskell.com/). But I want to share a small secret with you. You don\'t need to know Haskell at all to make your blog with Hakyll! If you have some programming experience (you can programm on some programming language and you know what VCS is) it will be more than enough to finish everything listed below. I would say that it could be more important to know HTML and CSS to customize website which will be generate by default, but more on that later.

#Step 2. Obtaining Hakyll

We are ready to get hakyll to become close to our goal. And [cabal][3] will help us with this. First of all, if our installation is fresh, it is a good idea to update cabal.

```{.prettyprint}

> cabal install cabal-install

```

It will spend some time on updating information about it\'s packages, and we will be ready for our next magic command:

```{.prettyprint}

> cabal install hakyll

```

And we are done! Or not. We should have hakyll after executing mentioned command, but I personally recevied an error that not everything went well and I haven\'t recevied greedily desired package. Unfortunally I didn\'t spend much time try to figure out that problem and just googled for error. And discovered that on Windows you probably need slightly different command to obtain hakyll:

```{.prettyprint}

> cabal install --flags="-unixFilter" --constraint="directory installed" hakyll-X.X.
X.X 

```

Instead of \'X.X.X.X\' should be some version: check the latest [here][4]. I could just assume that that error could happened if you are the Windows user like me :) And maybe one day I\'ll try to investigate that issue with more care. But you **should** be good after if not first, but after second command for sure.

#Step 3. Initializing site

Despite that this steps is rather clear described on [official hakyll page][5] I will repeat them here for consistency.
Previous step should award us with hakyll package so we can navigate now, in console, to our amazing future personal page location and initialize it:

```{.prettyprint}

> hakyll-init our_amazing_personal_site
> cd our_amazing_personal_site

```

Let\' see what we\'ve got. 

- site.hs file contains haskell code which will be later compiled into executable file, which grant us with ability to build site and run local server for preview. 
- index.html contains content for our *home* page.
- contact.markdown will be compiled into *contact* page.
- about.rst will be builed into *about* page. 
- _templates_ folder contains various templates which will be compiled into our future page\'s parts and injected in specfied locations. Also here you can find *default.html* which is basically our master page.
- _images_ folder contains images
- _posts_ folder contains posts in [.markdown][6] format.
- _css_ contains our default .css file and could serve as the only one spot to put your own future .css files. 

Of course you can change here everything, but before doing so please, make sure that you know haskell and read through site.hs. Also right now is a good moment to look around and check what is inside each of those files.

We are ready to compile site.hs into an executable and build our site!

```{.prettyprint}

> ghc --make site.hs
> site build

```

You can notice that more files appeared in our_amazing_personal_site folder. 

- *site.o*, *site.hi* and *site.exe* were produced by making site.hs file.
- *_site* folder contains our compiled and ready to run site. You can go inside and open index.html in your favourite browser. Congrats! :)
- *_cache* will contains cache information about visited site pages on localhost.

If you installed _hakyll_ with a preview server (this is default), you can now use

```{.prettyprint}

> site preview

```

which will run local server and you can access you site at [localhost][7]. In case site would complain about 8000 port busyness, you can run you server with:

```{.prettyprint}

> site server --port=5050

```

and access you site from [localhost](http://localhost:5050/).

#Step 4. Preparing repository

I hope that you already have your [github][8] account. If not, please go and register there. They have pretty 4-steps for newcommers. Anyway, after registering you account or simple log in you should create new repository for your_amazing_personal_site hosting. One important thing to remember, that name of repository should be in following format: 
__[your github username].github.com__

Now, run gitBush and navigate to ../our_amazing_personal_site/_site folder. We are going to create repository here.

```{.prettyprint}

$ git init
$ git add .
$ git commit -m "my amazing personal page with hakyll init"
$ git remote add origin [repository address github gently provided you with]
$ git push -u origin master

```

Phew\... We\'ve done this! :) You can go to your repository on github and check if your site source files are there. And you can of course just type __[your github username].github.com__ in you favourite browser address row and observe your site!

#Instead of Epilogue

I would like to apologize for my English. It is not my native language as you already figured out, but as my teacher once told me, it is could to start blogging and it will be improved. I hope it will be true :) Also I would like to give my apologies to all those amazing haskell programmers. In my blog-post I could said something wrong, or made some bad assumptions about haskell. If it is true, I\'ll try to be better next time :)

Hope you\'ve enjoyed.

[1]: http://jaspervdj.be/hakyll/ 															"hakyll"
[2]: http://en.wikipedia.org/wiki/Glasgow_Haskell_Compiler 									"GHC"
[3]: http://www.haskell.org/cabal/ 															"cabal"
[4]: http://hackage.haskell.org/package/hakyll 												"the hakyll package"
[5]: http://jaspervdj.be/hakyll/tutorials/01-installation.html#building-the-example-site 	"install site"
[6]: http://daringfireball.net/projects/markdown/basics										"markdown basics"
[7]: http://localhost:8000/																	"localhost"
[8]: https://github.com/																	"github"
