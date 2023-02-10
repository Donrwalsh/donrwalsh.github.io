---
layout: post
title:  "Political Linksmanship"
excerpt_separator: <!--more-->
---
If I keep randomly selecting problems from chapter 2, I'm going to rapidly run out of link-based puns. This week I timebox my solution to an hour.

<!--more-->

**Fri 2/10/23**
Working at Creed Interactive I am afforded one hour a week of personal development time which I generally allocate to working on these problems. This week I'm going to go a step further and completely timebox my efforts on this problem to this hour. At the end of which I will post what I have for better or for worse. Let's see how this goes, the timer starts now!

*Reads problem 2.2*. First thing that jumps out at me is the problem specifies a singly-linked list, which was notably left out of problem 2.1 as I recall. Continuing the theme of considering this problem through the lens of having worked on problem 2.1 recently, I also notice there are no stipulations on whether we can use supplementary data stores (i.e. a temporary buffer). That's ideal because the first thing that pops into my head makes heavy use of such a device.

First off, this algorithm will require traversing the entire linked list. Because our input is singly-linked, this is the only way we'll be able to know where the '$$k$$th last element' is since by definition that is a function of an elements distance from the final node in a linked list. The first idea I had will store the node values as it traverses the linked list. Either an array of length $$k$$ or a dynamic array that grows up to length $$k$$ but not further. This way once we reach the end of the linked list (that is, a node with a `next` value of null) we can consult our array to either find the desired value immediately or determine that the linked list is of insufficient length to be able to have a $$k$$th value.

Alternatively, we could traverse the linked list once to determine its length and then if it has a length of $$k$$ or greater, traverse it again up to the $$length - k$$ (give or take 1 to get the appropriate spot) position and report that value. This approach takes more time but requires less memory.

I am satisfied with these two possible algorithms, so I'm going to write up the solution now. *writes up solution*. I'm not the biggest fan of the `findKthValueDoubleIterate` function's requirement of the fallback to `null` values when blindly referencing `current.next`. The only way this code will end up referencing the next attribute on a node that is null is if the supplied $$k$$ value is negative, but even if I control for that by way of a conditional typescript.org won't let me get away with the assumption that it won't be null. Oh well.

Thinking about negative values for $$k$$ though... The first implementation still works just fine if $$k$$ is negative in that it will always return a value of `null` since the buffer length can never be negative. What about 0? Both my implementations return a `null` value for a $$k$$ of zero which feels accurate to me in that a $$k$$ of 1 is returning the very last node in the Linked List.

Looking at the solution in the actual CCI book there is a recursive solution that I did not think of. This solution follows a similar logic of the buffer solution in that it traverses fully and then once the end of the LinkedList is reached it consults available information to determine which is the desired value. I'm satisfied with the solution that I came up with, but it's always a good reminder to keep recursive techniques in mind.

This took me about 42 minutes after all is said and done. I am pleased with how this turned out and will probably continue to timebox when I am working in a chapter that deals with content I am confident on.