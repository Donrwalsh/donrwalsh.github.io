---
layout: post
title:  "Random Problem Generation"
excerpt_separator: <!--more-->
---
This week I tackle the randomly selected first problem from the final chapter of the book and take a first stab at binary arithmetic!
<!--more-->

**Mon 1/9/23**

Hesitantly, I reach for the padlock icon and give it a nervous click. Doing so will randomly select a new problem for me to solve and I kid you not it spits out 17.1. That's right, on week 2 of my challenge I am now going to attack the first of the 'Additional Hard Problems'. So it goes when you entrust your fate to the whims of random number generation.

**Wed 1/11/23**

Having thought about this on-and-off throughout the week, my instinct is to do binary representation of the two numbers and then mash them together with some binary-addition logic that is built without using arithmetic operators. I could build this using these functions:

- a function that converts a number to a binary representation.
- a function that converts binary representation to a number.
- a function that sums two binary representation of numbers.

This is not something I've spent a whole lot of time learning about, and so the third function might be as simple as a function that increments a binary number however many times. 

As an aside, I came up with a solution that totally ignores the spirit of the question:

{% highlight typescript %}
function sumTwoNumbersWithoutArithmetic(numA: number, numB: number): number {
    return Array(numA).concat(Array(numB)).length;
}
{% endhighlight %}

Anyway, I learned from reading about [The Absolute Essentials for Bit Manipulation in JavaScript](https://lucasfcosta.com/2018/12/25/bitwise-operations.html) that javascript supports quickly converting between numbers and binary:

{% highlight typescript %}
function numberToBinary(input: number): string {
    return (input).toString(2);
}

function binaryToNumber(input: string): number {
    return parseInt(input, 2);
}
{% endhighlight %}

This deals with string representations of binary which isn't ideal, but it'll do for now. Reading the section about summing two binary numbers working just like summing two base-10 numbers makes a lot of sense. I need to deal with the mashing of two binary digits and being able to decide whether I am carrying a value from one column to the next. 

Let's own the string representation of binary numbers for now, so our function's signature will look like:

{% highlight typescript %}
function sumTwoBinaryNumbers(numA: string, numB: string): string {
    //TODO: everything
    return "";
}
{% endhighlight %}

Hm, I wanted to kick things off by ensuring the strings were the same length but I'm actually not show how I would do that without using some form of arithmetic. 

Between the two binary numbers, whichever is longer will dictate how many times I need to iterate and decide what the output is for that column. I'm going to use a forEach here because a normal for loop in javascript uses `++` which isn't allowed under the terms of the problem so I'm going to turn these strings into character arrays and plan to work with an output character array that I'll translate when I'm done building it. Because addition is commutative, I don't need to care about the order of the input numbers, just which one is larger:

{% highlight typescript %}
function sumTwoBinaryNumbers(numA: string, numB: string): string {
    let arrayLonger = (numA.length > numB.length ? numA : numB).split('').reverse();
    let arrayShorter = (numA.length <= numB.length ? numA : numB).split('').reverse();
    let arrayResult: string[] = [];

    //TODO: sum the two arrays
    return "";
}
{% endhighlight %}

Next up I will iterate over `arrayLonger` and then consult `arrayShorter` to determine which value gets appended to `arrayResult` (remembering that the output is going to be backwards, so I need to reverse it before returning). This is what I came up with first:

{% highlight typescript %}
function sumTwoBinaryNumbers(numA: string, numB: string): string {
    let arrayLonger = (numA.length > numB.length ? numA : numB).split('').reverse();
    let arrayShorter = (numA.length <= numB.length ? numA : numB).split('').reverse();
    let arrayResult: string[] = [];

    let carry = false;

    arrayLonger.forEach((element, index) => {
        if (!carry) {
            if (element === '1' && arrayShorter[index] === '1') {
                carry = true;
                arrayResult.push('0');
            } else if (element === '0' && arrayShorter[index] === '0') {
                arrayResult.push('0');
            } else {
                arrayResult.push('1');
            }
        } else {
            if (element === '1' && arrayShorter[index] === '1') {
                carry = true;
                arrayResult.push('1');
            } else if (element === '0' && arrayShorter[index] === '0') {
                arrayResult.push('1');
            } else {
                carry = true;
                arrayResult.push('0');
            }
        }
    });
    
    return arrayResult.reverse().join("");
}
{% endhighlight %}

It is a little clunky to be sure, but the logic is all there (I'm taking advantage of the similarity between the two cases where one value is `1` and the other is `0` by making them the default 'fall-through' case to cut down on code). At least I thought it was until I saw that the output was incorrect. This is because I overlooked two things: One is that `arrayShorter` can be smaller than `arrayLonger` and so sometimes reading a value from the former will come out as `undefined` when I want it to be `0`. Two is that after all's said and done, I may end up needing an additional column beyond what was originally slated by the forEach loop so after the loop I consult the `carry` variable and if it is true I add a `1` into the final column. Due to the nature of binary numbers, this can happen at most once while processing a sum.

I also noticed that I had an additional bug where I neglected to add `carry = false` in the double-0 while carry is true section of the if statements.

Here's today's final product:

{% highlight typescript %}
function sumTwoNumbers(numA: number, numB: number): number {
    let binaryNumA = numberToBinary(numA);
    let binaryNumB = numberToBinary(numB);
    let binaryResult = sumTwoBinaryNumbers(binaryNumA, binaryNumB);

    return binaryToNumber(binaryResult);
}

function numberToBinary(input: number): string {
    return (input).toString(2);
}

function binaryToNumber(input: string): number {
    return parseInt(input, 2);
}

function sumTwoBinaryNumbers(numA: string, numB: string): string {
    let arrayLonger = (numA.length > numB.length ? numA : numB).split('').reverse();
    let arrayShorter = (numA.length <= numB.length ? numA : numB).split('').reverse();
    let arrayResult: string[] = [];

    let carry = false;

    arrayLonger.forEach((element, index) => {
        if (!carry) {
            if (element === '1' && arrayShorter[index] === '1') {
                carry = true;
                arrayResult.push('0');
            } else if (element === '0' && (arrayShorter[index] === '0' || arrayShorter[index] === undefined)) {
                arrayResult.push('0');
            } else {
                arrayResult.push('1');
            }
        } else {
            if (element === '1' && arrayShorter[index] === '1') {
                carry = true;
                arrayResult.push('1');
            } else if (element === '0' && (arrayShorter[index] === '0' || arrayShorter[index] === undefined)) {
                arrayResult.push('1');
                carry = false;
            } else {
                carry = true;
                arrayResult.push('0');
            }
        }
    });
    if (carry) arrayResult.push('1');
    
    return arrayResult.reverse().join("");
}
{% endhighlight %}