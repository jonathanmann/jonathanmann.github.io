---
layout: post
title: Verifiable Election System Demo Front-End
image: http://jonathanmann.github.io/public/img/voting_system_frontend.png
excerpt: In an earlier post, we looked at the mechanics behind creating an election system where the results could be verified by any third party while still protecting voter privacy. In this post, we'll look at a demo implementation of a user interface for this system.
---

In an [earlier post](http://jonathanmann.github.io/2015/08/29/transparent-verifialbe-private-elections/), we looked at the mechanics behind creating an election system where the results could be verified by any third party while still protecting voter privacy. In this post, we'll look at a [demo implementation](https://github.com/jonathanmann/blog_examples/tree/master/Javascript/election_system_demo) of a user interface for this system.

### Live Demo

You can view a live demo of this implementation [here](https://cdn.rawgit.com/jonathanmann/blog_examples/master/Javascript/election_system_demo/index.html).

### Voting Process Description

![ballot](http://jonathanmann.github.io/public/img/voting_system_frontend.png)

When the voter enters the booth, the ballot appears. The voter can select from the available options. When the voter touches an option, the selected option becomes highlighted. The voter can then confirm the selection with the bottom button. The system then routes to a confirmation screen where a unique identifier is presented along with the ticket the voter selected. A receipt matching the information on the confirmation screen would then print so that the voter could later use the information to verify the the vote was accounted for accurately.

The printed receipt might look like this :

2B182210-64CC-48AD-9022-DFA702A6C641 | NEUTRAL PARTY

Although the process would be over at this time, in the [live demo](https://cdn.rawgit.com/jonathanmann/blog_examples/master/Javascript/election_system_demo/index.html), I added a button to "View Election Result". 
  

### Result Verification Description

The [election results screen](https://cdn.rawgit.com/jonathanmann/blog_examples/master/Javascript/election_system_demo/index.html#/result), is a demo of what news agencies and watchdog organizations could put together from the election data after the election results were released. Voters could look up the unique identifier from their confirmation cards and verify that their votes were accounted for accurately.
