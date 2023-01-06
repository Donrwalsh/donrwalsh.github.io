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

**1/6/23**

Question 1.1 asks to implement an algorithm and I'm working a lot with typescript these days so I decided to implement my solution in that language. For CLRS solutions I've taken advantage of Jekyll's built-in syntax highlighting so I figure it makes sense to use that here.

I'll be candid here and admit that I am familiar with this question and the book's solution, so my mind wants to jump to character encoding details. First though, I'm going to construct a simplistic implementation. My first version looked like this:

{% highlight typescript %}
function hasAllUniqueChars(subject: string): boolean {
    let foundChars: string[] = [];
    for (let i = 0; i < subject.length; i++) {
        if (foundChars.includes(subject[i])) {
            return false;
        } else {
            foundChars.push(subject[i]);
        }
    }
    return true;
}
{% endhighlight %}

I have developed this habit of trying to use `Array.map` whenever I instinctively reach for a for loop, but in this case since I'm interested in returning a value upon identifying a duplicate char I don't think a map function is appropriate. I looked into using a forEach function as well, but that doesn't break the iteration on return so it won't suit my needs either.

I interpret the stipulation that you can't use additional data structures to mean that my use of `foundChars` is now outlawed. No worries, I can perform the same sort of logical approach by consulting the rest of the string.

{% highlight typescript %}
function hasAllUniqueChars(subject: string): boolean {
    for (let i = 0; i < subject.length; i++) {
        for (let j = i; j < subject.length; j++) {
            if (subject[j] === subject[i]) return false;
        }
    }
    return true;
}
{% endhighlight %}

I originally wrote that this new approach ups the runtime from $$O(n)$$ to $$O(n^2)$$ but I'm actually thinking that both of these solutions have a runtime of $$O(n^2)$$. My reasoning for the runtime of the first one is that the foundChars array will eventualy grow to be $$n$$-length which I think gets treated the same as an array of length $$n$$. I consulted the book's section on Big O notation briefly and it looks like this is the case. Nifty!

It occurs to me that maybe using `foundChars.includes` in the first solution is cheating. At first I was worried because the structure of the code hinges pretty heavily on interpreting as a boolean whether or not to return or push the char in question, but I thought about it for a moment and I would just place the `.push` beyond where the secondary for loop runs so that it basically behaves as an `else` anyway. Looks like this:

{% highlight typescript %}
function hasAllUniqueChars(subject: string): boolean {
    let foundChars: string[] = [];
    for (let i = 0; i < subject.length; i++) {
        for (let j = 0; j < foundChars.length; j++) {
            if (subject[i] === foundChars[j]) return false;
        }
        foundChars.push(subject[i]);
    }
    return true;
}
{% endhighlight %}

I like this one better than the first one because `.includes` masks a piece of the logic of this algorithm.