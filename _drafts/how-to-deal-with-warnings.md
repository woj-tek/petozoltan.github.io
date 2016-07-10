In every software project's life there is a moment when the team decides to install a Sonar server and to do something with warnings in order to increase code quality. ***And then all of the teams will fail.*** This is a typical scenario:

* We work on the software for a long time, until the first or second "big release".
* One or two years after the project start we install the Sonar server.
* The first schock comes when we see the high number of warnings, which is usually 10-20 thousand.
* We realize that we have no chance to fix them, so we come up with a strategy to *decrease the number of warnings*. Usually by fixing the critical and major issues first.
* We get the second schock after half or one year again when we see that nothing happened with the warnings. Their number has even increased.

Does it sound familiar? Let's see what are here the mistakes, and the lessons learned. Finally I suggest a new way when dealing with this situation.


### Take care of warnings from the project start

The most obvious mistake that the Sonar - or, more generally, the controlling of warnings - is started  when it is too late, when there are way too many of them. I wonder, why we do this mistake even at the 1 millionth software project when it can be known.

Many other measures and tools are usually in use right from the project start: version control system, continuous integration, unit tests, behavioral tests, bug tracking system, documenting tool, etc. Except for the checking of warnings...


### Do not hide warnings in the IDE

This is the most painful one. Developers do not turn on the displaying of warnings in their local development tools. They hide the warnings, so *they continuously commit a lot of warnings* all the time. Even while they are talking about how to decrease their count, they increase it.

Unfortunately the default setting of IDEs is that warnings are turned off, suggesting that this is the good approach. But it is not. I suggest that the "default setting" should be to turn on all of them and then hide some of them. Which ones should be ignored can be discussed by the team.


### Understand what warnings are

It seems that *warnings are still the stepchildren of software development*. Something annoying that can be ignored. The root problem is that we do not understand what warnings are.
 
Warnings point to real problems in our source code. ***Warnings are potential bugs.*** Actually they *are* bugs, because most of the bugs are caused by incorrect code parts, which could be detected via warnings. Moreover, warnings point to deeper structural problems in the code, which are not simple to fix. Probably that is why we do not like them. (For example, unused parameters are usually a sign of bad class hierarchy.)

There is no fundamental difference between warnings and errors! They differ only in the arbitrary level what we assign to them. You can set it in your IDE.

And I do not have to mention that warnings should not be fixed via `SuppressWarnings`...


### Add code checkers to your IDE

I have heard this buzzword many times: "We will turn on the Sonar", suggesting that after this everything will be fine. But it will not, since Sonar will not fix the warnings only show them. 

What does exactly Sonar server do? 

* It executes some static code checkers, and displays their results. The code checkers are usually these ones: *CheckStyle*, *FundBugs* and *PMD*.

* It executes the code checkers on the code which is already committed into the version control system.

These static code checkers are also available as pluging for our IDEs. So I simply suggest to install them locally at the developers and execute them prior to the commits at least on the new or modified code parts. So we will not commit "Sonar warnings" any more!


### Always keep warning count on zero

We have a strict rule that the code base committed to the repository must contain 0 compilation errors. We also require that the count of failing unit test is also 0, so if there are any, they must be fixed immediately. We should deal with warnings on the same way.

A simple "psychologycal" reason is that nobody will notice if the warning count changes from 16482 to 16492, but it is easy to detect a change from 0 to any number.

I suggest to apply this approach even when we start to check warnings in the middle of the project, when we have tens of thousands:

1. Turn off all warnings for all modules at first.
1. Clear warnings or modules one-by-one:
  1. Decide to clear one warning level or one warning type or one code module. 
  1. Turn on warnings only for this. 
  1. Fix the warnings immediately.
1. Repeat step 2.