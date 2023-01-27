---
layout: post
title:  "An Easy Pill to Swallow"
excerpt_separator: <!--more-->
---
For this week, Problem 6.1 is a classic logic puzzle that fits the bill of needing something that consumes little time.
<!--more-->

**Fri 1/27/23**

I am short on time this week, so I'm going to break protocol and pick the chapter from which I will solve a problem rather than randomly selecting one. I'm going to go with Chapter 6 because logic puzzles are fun and the first one of the chapter should go suitably quick.

*Reads Problem 6.1*. As luck would have it, I am familiar with this problem but I don't remember where from. Because of that, I will walk through the deduction process from the perspective of someone who doesn't know the answer.

Consider the most impactful restriction: being able to use the scale just once. If we remove this restriction the problem becomes quite simple. We could weigh groupings of $$n/2$$ bottles and disqualifying groups that clearly don't contain the bottle with heavier pills. This would take in the worst case 5 weighs if we always guessed wrong. But we can't do that and so we must construct a scenario wherein when we perform the single allowed weigh the answer is immediately apparent.

There is another unique characteristic of the problem to consider. The object in question is pill bottles and the item that varies in weight is the pills inside the bottle and not the bottles themselves. It is not stated how many pills each bottle contains but in general we can probably safely assume that they contain a high number of pills. If, for instance, the problem dealth with jars with colored balls inside we would have no reference of how many colored balls each jar contains. Instead, we've been given a real-world object that many are familiar with and so making an assumption that each bottle contains at least, oh let's say $$19$$ pills is not outlandish. Why $$19$$ pills? I'll explain that in a second.

So we have 20 bottles to work with which is a lot. Let's reduce that to 2 bottles and see what we can come up with in the hopes that it might lead us down some sort of inductive trail. If I had two bottles and one of them surely had the heavier pills, if I took one pill from a bottle and weighed it I would know immediately which bottle had the heavier pills by either observing the pill weigh in at 1 gram (indicating the bottle I didn't choose from contains heavier pills) or by observing the pill weigh in at 1.1 gram (indicating that I obviously chose from the bottle containing heavier pills). This is not very useful because the tactic completely collapses as we add more bottles to the equation, but it gives us a helpful footnote in that we can perhaps leave one bottle out of the weighing entirely and deduce that the omitted bottle is the culprit.

So let's talk about how the problem changes when we add that 3rd bottle. By leaving one bottle to the side and selecting a pill from the other two bottles, we're in a difficult spot because if we didn't set the bottle with heavier pills to the side, there is no way to differentiate from which bottle the pill that is 1.1 grams came from. So we'll modify our approach slightly and instead of grabbing just one pill from either bottle we will grab one pill from the first bottle and two pills from the second. Since the parameters of the problem state that all pills in the offending bottle will be 1.1 grams, we will immediately obtain an unambiguous answer to our question upon weighing the three pills. If the weight is 3 grams then the bottle we did not take pills from contains heavier pills. If the weight is 3.1 grams then the bottle we took one pill from contains heavier pills. And finally, if the weight is 3.2 grams then the bottle we took two pills from contains heavier pills. 

So this solution is valid for 3 bottles, but what about the original question where we are dealing with 20 bottles? This is where the magic number $$19$$ comes from. We will be setting one bottle aside and selecting between $$1$$ and $$19$$ pills from each of the other bottles (hopefully labeling which bottle is which and keeping the piles of pills distinguishibly separate throughout the exercise). Then we weigh the $$210$$ pills we selected and note the weight. Then the bottle from which we took $$(weight - 210)*10$$ pills from is the bottle that contains heavier pills.

