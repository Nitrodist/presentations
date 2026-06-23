# (Archived) Presentations I've given 2015-2017

This repo has presentations I've given from 2015 to 2017.

The presentations are made with the awesome
[Deckset](http://www.decksetapp.com/) app which uses a markdown file to
generate a slideshow. I guess it's still an app (writing this message in 2026
after using the Deckset app 2015 through 2017 so I'm dating myself a bit here -
and you, dear reader) 😅

### [Stupid command line tricks](2015-08-21-stupid-command-line-tricks/stupid_command_line_tricks.pdf)

## 2015-08-21

This presentation I gave at a talk night for the Toronto Ruby Brigade. It
focused on using the command line (e.g. a bash or zsh shell) effectively.

It was actually fun blowing peoples' minds haha. Being able to use an text
editor before running a command!? Madness!

Man throughout these presentations I always leave my Twitter handle. I'm so
glad I deleted Twitter.

## [Conway's Game of Life presentation @ TRB hacknight workshop](2015-09-30-code-retreat/2015-09-30-code-retreat.pdf)

### 2015-09-30

Myself and David Andrews of the Ryatta Group hosted a session teaching
programmers old and new about software development techniques with pair
programming and test driven development at the Toronto Ruby Brigade in November
of 2015.

The goal of it was to implement the rules of Conway's Game of Life and then
compare and contrast the techniques that people actually used with ones that
David and myself knew and taught.

I had a lot of experience with Conway's Game of Life at other code retreats and
workshops so I suggested it to David that we use it for our hack night's
workshop. Infinitely extendible too - ok, you implemented the rules.. can you
display it in a web browser, and more challenges.

In the presentation I show what the game is and then we went right into it in
real life with people pairing off to work on the problem.

## ['Making it in the biz' - Talk to current RRC BIT students](2015-11-17-rrc/rrc.pdf)

### 2015-11-17

In 2015 I returned to Winnipeg for a visit with family and friends. I think I
also attended The Long Con in the same time frame as my visit to Winnipeg from
Toronto. At the time I was working for theScore as a team lead running a full
stack Ruby on Rails and devops etc. and running a Ruby ([the programming
language](<https://en.wikipedia.org/wiki/Ruby_(programming_language)>)) user group.

## [Ungemifying your projects](2015-04-06-ungemifying-your-projects/2015-04-06-Ungemifying-your-projects.pdf)

### 2015-04-06

Haha, I read through this presentation today in 2026 and it evoked a lot of
memories. Back in the day at my first stint at theScore we were a pretty tight
knit team that was in growth mode, so a lot of hiring of smart and likeable
people was happening. We were 50 people running a start-up and it was fun!

This talk/presentaiton that I gave was about an internal problem we had at
theScore where we had several rails projects that connected to the same
database, thus we wanted to have ActiveRecord models for the database separated
from the downstream Ruby on Rails projects and then the projects can re-use
this shared library of model-layer code.

> Active Record is part of the M in
> [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) -
> the model - which is the layer of the system responsible for representing
> data and business logic. Active Record helps you create and use Ruby objects
> whose attributes require persistent storage to a database.

Let's for a moment be more technical and to explain the exact problem. I guess
you could go into the PDF presentation to understand it, but it lacks the
internal monologue that I had for myself when I was reviewing the presentation
in 2026 haha.

In the ruby programming language we have a Gemfile and a Gemfile.lock file that
lists the program/your rails app's ruby library dependencies, known as gems.
Internal gems can be used at companies and referenced by git repo, branch,
commit, etc. so this allows for easy internal publishing and use of internal
software libraries. The advantage here is that you do not need to run a gem
server like rubygems.org, the default ruby gem server (which your Gemfile most
likely immediately references on the first line with `source "https://rubygems.org"`.

Though a lot of companies I worked at did do the whole internal gem server
thing, it is, and was, a massive waste of time given the headache of
maintaining one for few gains. In fact, you were signing yourself up for
downtime, haha.

- 2017-02-07 - [Production Debugging in AWS Elastic Beanstalk](2017-02-07-production-debugging-in-aws-elasticbeanstalk/production-debugging-in-aws-elasticbeanstalk.pdf)

This talk I gave walks through debugging a Ruby on Rails app and a second Ruby
on Rails app, the techniques used, technologies, commands, etc.

In 2017 I had been working for SERMO for about a year. During that time I
continued to host and run with my friend Luke Reeves the Toronto Ruby Brigade,
which was a in-person ruby user group meetup with workshops and talks. I gave
talk about debugging this tricky situation where the ruby code for base64
encoding adds a newline every 80 (?) characters if the data being encoded is
long enough.

In this case, we were using a http library where you specified the http
_Authorization_ header manually and were tasked with base64 encoding the header
value, so the bug crept in.

I think we didn't find it until we deployed it to production. Our production
credentials for the expected username and password were juuuuuusssst long
enough to run into the ~80 character limit before that dang newline was
inserted.

Of course it happened only in production... haha.
