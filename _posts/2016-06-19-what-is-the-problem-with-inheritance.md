---
layout: post
title: "What Is The Problem With Inheritance?"
date: 2016-06-19
---
I almost always find very hard and annoying to maintain the class hierarchies we write. And I am constantly thinking on the reasons, why. Inheritance is one of the basic principles of object oriented programming, so it may sound strange that there is a problem with it. Of course, inheritance is good but the way we use it may not be good. Let me explain it through an example.

### Feature development

Imagine that you are a programmer and you have a task to implement a certain feature. What do you expect?

| Specification: | The feature is carefully found out and discussed by one or more business analysts. |
| Design: | Prior to the coding the solution is well planned by technical people like architects or by the developers themselves. At least verbally but possibly in written documents. | 
| Implementation: | The feature is not only implemented well by a good programmer, but it also fulfills the requirements. | 
| Test: | The implemented program is tested on at least one level but more levels are better (unit, functional, integration, etc. tests). | 

Usually these steps happen in a serious software company.

### Framework development

When you create class hiearchies to use them in the future, and to use them by other developers, then you really create a ***framework***. Especially the presence of abstract classes show that others have to *"put their classes under this hierarchy"* and if they do they will be fine. That is what i call a *"framework"*.

So imagine now that you have to implement a framework. Wouldn't you expect the same conditions as in the feature development?

* Specification
* Design
* Implementation
* Testing

Yes, you would.

### Inheritance in reality

And now let's see how and why programmers create class hierarchies and abstract classes in reality. They work on a certain feature and create classes for it. During the coding they might say:

> "Oh, it is so generic, I extract it to a parent class."

Or, even more often they discover the similarities between a new and an existing class and they say:

> "I put the equal parts into a common base class and the differences into abstract methods."

Or they may have other complex reasons including the usage of a design pattern (which is at least a more judicious approach).

But remember, this is a framework development. What is with the expected conditions?

* Specification: No
* Design: No
* Implementation: Yes
* Testing: No

A little bit more detailed:

**Specification**: The intention of such framework is always this one:

> "It will be good for the next developer / modification / sub-class / etc."

But unfortunately it will not.

**Design**: There is only an ***ad hoc*** design. The programmer has a quick idea and it is implemented. And the idea usually does not exceed the "common base class" antipattern. 

Moreover, it does not fullfill the specification. (Remember: "It is generic." or "It will be good for the future."). Instead of that, it usually only freezes the differences between some already existing specific classes.

**Implementation**: There it is, but not in the terms of fullfilling the requirements since there are none.

**Testing**: The developers usually test only the sub-classes, which involves more or less the code from the parent classes too. But the parent classes - especially the abstract ones - are not tested at all. They are not tested like any other classes with a well defined and enclosed functionality.

### Related posts

* [When To Avoid Inheritance?](http://petozoltan.github.io/2016/06/18/when-to-avoid-inheritance.html)
