---
layout: post
title:  "The Missing Link"
excerpt_separator: <!--more-->
---
Problem 2.1 is a gentle re-introduction to Linked Lists. Marvel as we reduce the complexity of $$\pi$$ by removing pesky duplicate digits!
<!--more-->

**Tue 1/17/23**

This week's random assignment is question 2.1, the first in the chapter on Linked Lists. This question asks to remove duplicate values from an unsorted linked list. The follow-up question asks how this might be done if a temporary buffer is not allowed. My first thought is that this question does not specify whether the linked list is doubly-linked, so I will assume it isn't. 

First things first. I have never built a linked list data structure in typescript before because I've never had the need to, so that seems like a reasonable place to start. So we'll need a Node class that holds onto a value and possibly points to the next Node in the sequence:

{% highlight typescript %}
class ListNode<T> {
    public next: ListNode<T> | null = null;
    constructor(public data: T) {}
}
{% endhighlight %}

Next, we'll need a class for the Linked List itself:

{% highlight typescript %}
class LinkedList<T> {
    constructor(public head: ListNode<T> | null = null) {}
}
{% endhighlight %}

Hard to get much more basic than that.  In order to solve this challenge, I'm going to need to construct a Linked List with a variety of values some of which are going to be duplicates. It'll also be nice to be able to quickly review the contents of a Linked List so let's implement those two methods on our LinkedList class:

{% highlight typescript %}

class LinkedList<T> {
    constructor(public head: ListNode<T> | null = null) {}

    public appendToTail(valueToAppend: T) {
        let nodeToAppend = new ListNode(valueToAppend);
        if (this.head === null) {
            this.head = nodeToAppend;
        } else {
            const getLast = (node: ListNode<T>): ListNode<T> => {
                return node.next ? getLast(node.next) : node;
            }
            let lastNode = getLast(this.head);
            lastNode.next = nodeToAppend;
        }
    }

    public print() {
        let output = "head: "
        let n = this.head;
        while (n !== null) {
            output += "[" + n.data + "] -> "
            n = n.next;
        }
        output += "null";
        return output;
    }
}

{% endhighlight %}

**Wed 1/18/23**

Using these two methods, I can generate an unsorted Linked List to use as a generic input for solving the problem. My gut says use random number generation, but it would be better to stick with a static input so I'm going to use the first 50 digits of $$\pi$$:

{% highlight typescript %}
let ll = new LinkedList<number>;

for (let i = 0; i < 50; i++) {
    ll.appendToTail(Math.floor((Math.PI * Math.pow(10, i))) % 10)
}

console.log(ll.print());
{% endhighlight %}

This outputs: `"head: [3] -> [1] -> [4] -> [1] -> [5] -> [9] -> [2] -> [6] -> [5] -> [3] -> [5] -> [8] -> [9] -> [7] -> [9] -> [3] -> [2] -> [8] -> [0] -> [6] -> [4] -> [8] -> [8] -> [0] -> [6] -> [4] -> [8] -> [6] -> [2] -> [6] -> [2] -> [8] -> [0] -> [6] -> [6] -> [2] -> [2] -> [6] -> [2] -> [2] -> [8] -> [4] -> [4] -> [8] -> [0] -> [2] -> [8] -> [0] -> [2] -> [4] -> null" `

Using this as an input, it should be straightforward to see if my solution is doing what I need it to do. Heck, I could even craft a method to specifically check that my solution produces the desired output by just solving this one by hand. That's probably unnecessary, but I'll keep it in mind as an option for static code checking.

Before getting into the algorithm to solve this problem, I'm going to need a way to remove a node from a Linked List. In an effort to be forward-looking, I'll empower this method to be able to remove the head node even though that won't be necessary for this particular problem. I think I will set up this method to remove a Node by position in the Linked List. This might cause problems when I get around to removing while traversing, but I will revisit this plan if I need to (though at this point in time I can't really think of an alternative).

{% highlight typescript %}

class LinkedList<T> {
    //...

    public removeNode(position: number) {
        try {
            let currentNode = this.head;
            
            if (position === 0) {
                this.head = currentNode!.next;
            }

            for (let i = 1; i < position; i++) {
                currentNode = currentNode!.next;
            }
            currentNode!.next = currentNode!.next!.next;
        }
        catch (error) {
            throw new Error("Unable to remove Node at position " + position);
        }
    }
}
{% endhighlight %}

I'm going to make the removeDuplicates code a separate function since it will be manipulating the Linked List:

{% highlight typescript %}
function removeDuplicates<T>(input: LinkedList<T>) {
    let foundValues: Array<T> = []
    let nodesToRemove: Array<number> = [];

    let workingNode = input.head;
    let index = 0;
    while (workingNode !== null) {
        if (foundValues.includes(workingNode.data)) {
            nodesToRemove.push(index);
        } else {
            foundValues.push(workingNode.data);
        }
        index++;
        workingNode = workingNode.next;
    }
    for (let i = 0; i < nodesToRemove.length; i++) {
        input.removeNode(nodesToRemove[i] - i);
    }
}
{% endhighlight %}

The `input.removeNodes(nodesToRemove[i] - i)` comes from the notion that every time we remove a node all nodes with a higher position are shifted down by 1. The `nodesToRemove` array was built sequentially, so we know it is in strictly increasing order.

The result of running this function with the $$\pi$$ Linked List as an input appears to be successful: `"head: [3] -> [1] -> [4] -> [5] -> [9] -> [2] -> [6] -> [8] -> [7] -> [0] -> null" `

Great, that's the first half of the problem. Now to think about how I'd do this without using a temporary buffer. . .

**Fri 1/20/23**

So my thinking about this follow-up question is that we can sort the Linked List and then remove duplicates based on any found sequences of matching values. That didn't feel right, because after doing so there would be no way to return to the unsorted form with duplicates removed. So I took a look at the book's solution and it holds onto a node and compares the rest of the Linked List to that node, removing duplicates as it finds them. This is peculiar to me, because isn't that a buffer?

{% highlight typescript %}
function removeDuplicatesNoBuffer<T>(input: LinkedList<T>) {
    let currentNode = input.head;
    let workingNode;

    while (currentNode !== null) {
        workingNode = currentNode;
        while (workingNode !== null) {
            if (workingNode.next !== null && workingNode!.next!.data === currentNode.data) {
               workingNode.next = workingNode!.next!.next;
            } else {
                workingNode = workingNode.next;
            }
        }
        currentNode = currentNode.next;
    }
}
{% endhighlight %}

So we start with `currentNode` as the head of the Linked List and then inspect the rest of the Linked List for any duplicate values and remove them on the spot when we find them. I don't use the removeNode method because it gets troublesome to keep track of positions and I'm working with the Nodes themselves anyway. After traversing the entire Linked List, the `currentNode` steps forward one Node and repeats the process. The output is the same as the solution that makes use of a buffer: `"head: [3] -> [1] -> [4] -> [5] -> [9] -> [2] -> [6] -> [8] -> [7] -> [0] -> null" `