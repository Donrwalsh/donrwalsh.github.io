---
layout: post
title:  "Mess with the Test..."
excerpt_separator: <!--more-->
---
I love testing. No joke. So this week was a fun one for me and in case you're wondering the title is in fact a Hackers reference!

<!--more-->

**Sun 2/6/23**
First things first: I'm publishing this outside of the week that I'm supposed to have worked on this. I spent some time reading this problem and pondering it throughout the week but never found the time to sit down and write up my thoughts so I'm doing that now. I'm marking this post with a publishing day of yesterday because this represents work I did last week, though I do concede that I'm getting very loosey-goosey with when I'm doing this work and I would like to see a bit more adherence to the original plan I had set out for myself. Ok, onto the problem!

This week's problem (11.1) was randomly generated and the subject matter of testing is something that I've found to be very interesting in my career. I'm excited to read what this book has to say about testing but alas did not find the time to do so last week and so I mostly just dove in on the problem itself. Given that the code snippet we're looking at is C++, the majority of the diving in involved looking up syntax that I knew at one point but is now a distant memory.

So bit-by-bit, here are the bits that I looked into:

- `i--`: Based on context, it's clear that this is some form of `--i`, but I needed a quick search to remember that it indicates we do the subtraction first and then work with the `i` value that is produced by the operation.
- `unsigned int`: Google helpfully explains that an unsigned int only represents non-negative integers.

So that's enough to notice an issue. The loop as defined will only terminate when `i` holds a value that is less than $$0$$, which is not possible with the way we have typed `i`. I incorrectly assumed this would result in some kind of error. The solution from the book itself explains that this will result in an infinite loop as `i` remains at $$0$$ no matter how many times we try to decrement it. Interesting!

- `printf("%d\n", i)`: This syntax is familiar and I know that it indicates that the `%d` placeholder (apparently called a 'format specifier') will be replaced with the value that `i` holds. At first I thought this was a int-inside-a-string issue, but that's just my python sensibilities showing through and a cursory search demonstrated that this sort of things is routine.

But reading further about all the different format specifiers that are available, I noticed that the `%d` specifier is for signed decimal integers which is unnecessary when our `i` value is unsigned. This feels like another error, though certainly of a much smaller magnitude than the first one. The first issue will cause this loop to run indefinitely while the second issue will probably result in an accurate but sub-optimal performance.