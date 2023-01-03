---
layout: post
title:  "First Week"
excerpt_separator: <!--more-->
---


<!--more-->

**1/3/23**

I started out by taking the built-in drafts functionality of Jekyll for a spin. Pretty cool way to work on posts locally while awaiting publishing. Just need to run the usual `jekyll serve` command but with the `--drafts` flag and it will treat the draft as though it were published today without impacting what's actually live out on prod.

One of the big things I need to do this week is establish a repo for the CCI problems I'm going to solve. I don't see much reason to deviate from the pattern that I built for CLRS. It will take some manual work to stand up, but I really enjoyed how simple it was to work on a new problem solution within the site the way that I built it. I started by copying the structurally important stuff from the CLRS repo and tweaking the card presentation to suit the unique CCI needs. I removed the differentiation between exercises and problems and added in chapter titles. From there I built out the YAML files for the overall list of chapters and then one for each individual chapter with an established slot for every question based on what's in the book. To be frank, I worked really hard to establish the pagination that gracefully hops over gaps in solutions and I find a little bit of manual work more tolerable than attempting to rebuild something that I know works. Especially since this will get me quicker to a comfortable spot of being able to work the problems. 

This whole process did not take very long at all. I capped everything off by selecting the padlock icon to represent CCI (unlocking == cracking, get it?) and re-adding the random assignment selection functionality. I'm going to kick things off with 1.1 this week, but the intent is to do a randomly selected question from here on out. We'll see how plausible that is!