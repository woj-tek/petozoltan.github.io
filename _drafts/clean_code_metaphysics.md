# Why is it hard to convince programmers about clean code?

The deeper reasons.

## Two Types of Programmers

Our brains are different. Two basic types:

* Those who are inherently clean coders
* Non clean coders

CCs may always try to do CC activities even before they are aware of it. When they finally read about CC they might have the "aha" feeling.

Non-CCs are not simply do not CC but it is also hard to convince them about it.

## Clean Code's Name

Clean Code may be misleading. It is not "code beautifying" but it is the quest to find the one-and-only correct implementation. I would call it

> Correct Code

## What Is This Code Doing?

The common thesis is that we constantly ask this question when readin and writing the code. ("The number of WTF-s"). But programmers may answer:

*"It goes through this list, creates that map and then calls this method, etc."*

While CCs expect something like:

*"It collects all active items."*
 The reason is that the above question may be simply *ambiguous*. Lets' replace it with the question:
 
 > Why is this code doing what it does?

## When is the code 'good'?

* NCCs may say good = working
* CCs may say good = working + something more

Working really means that it is working *now*.

> Good = Works + Time 

Good = It works and will work in a constantly changing code basis. 

It is like writing code on a moving paper or painting on the surface of a river.

And when will it work in time? That's the root of clean code:
* simple
* readable
* non-ambiguous
* granulated
* tested
