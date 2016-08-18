---
layout: post
title: "When To Avoid Inheritance?"
date: 2016-06-18
---

***

* TOC
{:toc}

***

A huge problem of software development is that the code becomes over-complicated and hard to maintain. I see that the ***overuse of class inheritance*** is one of its biggest reasons. Unfortunately developers have an affection to create class hierarchies and abstract classes.

That is why I tried to collect signs and hints that can show when inheritance is not necessary. I also try to tell which clean code principles are broken in such cases. Of course all of this sentences are worth for a longer description but now I can collect only the brief list with very short explanations.


## What Not To Do


#### Do not create parent class only for common methods

Common methods could go into a simple class which is used by reference. And if they could, they should.

Parent and child classes must be the variants *of the same type*. So if a parent is only a bunch of common methods they are probably not.

#### Do not create a parent class only to inherit common members (class variables)

Repeating class variables and injected instances is not code repetition. It is a misunderstanding. The same functionality must not be implemented more times. But declaring references can be explicitly expressed, even if copy-pasted.

#### Do not create parent class if you find that you cannot add children

The class hierarchy is very wrong if the child classes:

* have empty implementations for the abstract methods, 
* do not use input parameters of the inherited methods,
* must override already implemented methods.

#### Do not create class hierarchy if you got warnings

This is similar to the previous case, because you might get warnings about unused parameters, empty blocks, etc. Of course, you should *turn on warnings* to see them.

#### Do not create parent class if you have to call `super` or pass `this`

If you 

* have to call `super` but not in a constructor, or 
* have to pass `this` from parent to child or opposite, 

then parent and child just simply call each other as independent classes. No need for inheritance between them.

#### Do not create parent class if you find that it must be modified when a child class is added or modified

This is a violation of the *Open/Closed Principle*. The parent class should not be modified when a new descendant class is added.

#### Do not create parent class if you do not plan to use it as a declaration type

In this case the parent type is not necessary, therefore it should not exist.

#### Do not create a parent class only to do something on an abstract level

Doing abstractions is recommended. But the most simple abstraction is a method. There is no need to put methods in a parent class.

#### Do not create abstract parent class if you can remove its abstract methods and the program still compiles

Try to remove the abstract methods and the `@Override` annotations from the child classes. If the entire application compiles then it is a clear sign that the abstract methods were unnecessary. Then the class also does not need to be abstract. Then check that the class still does what its name promises without the abstract methods.

#### Do not create abstract methods if they are neither public nor called in the abstract class

These are absolutely unnecessary, while they are mandatory for the child classes.

#### Do not create parent class if it has no public interface

If there is no public interface then this class type will be definitely not used. So it is not necessary.

Additionally the child classes must have public methods so they will not be in an “is a” relation.

#### Do not create parent class if it has no own behavior

A class must behave like its name tells. Classes in a hierarchy must have the same behavior. E.g. a Converter's all parents and children must be all Converter too. A “bunch of methods” is not a behavior.

#### Do not create a parent class when you cannot unit test its behavior

#### Do not create a parent class if you cannot find a good name for it

Abstract..., Base..., Common... are no good names. There is no "abstract" functionality or behavior.

#### Do not create parent class if it is not cohesive

If its members can be split into groups that use each other but only in the same group than they should go into separate classes. But composition should be used then.

Cohesion is basically a synonym of the *Single Responsibility Principle*, which should not be violated.

#### Prefer composition to inheritance

See Effective Java book.

#### Use interface instead of base class if a common interface is really needed

#### Create polymorphic classes only if you can exactly name the design pattern with polymorphic classes you want to use

#### Do not create polymorphic classes if you cannot prove that it is really necessary

If you cannot prove that this is the only solution for an implementation. Polymorphic classes are a very expensive solution. Chose a cheaper solution if you do not have to do the more expensive one.

#### Do not create a parent class for a small benefit or obvious code

For example, only to have a loop over a collection is a small benefit, but you chose an expensive solution for that, when using inheritance.

#### Do not create parent classes just because you will configure the specific class in the injection framework

This is a wrong level of abstraction. If a class needs a specific type then inject that type.

#### Do not create abstract methods for non-procedural differences

If they differ only in data then use proper method parameters.

* Wrong: `@Override getMyType() { return SPECIFIC_TYPE; }`
* Less wrong: `super(SPECIFIC_TYPE}`
* Good: No subclass at all.

#### Do not create child classes if they contain only non-procedural differences

If only values are different it is no reason for a class. Classes are for procedural differences.

#### Create separate interface for the parent and child classes instead of inheritance

For example the parent has the public interface *A* (a set of public methods) and it has the set *B* of abstract methods. The children practically have the interface *B*, a different interface than *A*. So the hierarchy can be simple refactored into a service/subservices or runner/runnables architecture.

#### Do not create abstract framework on the top of a framework

Do not create wrappers or override methods with slightly different working. Instead, use the underlying framework correctly as it is.

#### Never create parent class for test classes

Test cases must be simple and *independent*.


## What To Do When Using Inheritance


#### Make methods final

"Make implementation mandatory or prohibit it." (Effective Java book)

Overriding an implemented method is a nonsense and it is also a dangerous. You must not override an existing implementation of a method. The parent class is closed, complete and tested. If you change only a portion of it, it can be broken.

And if you add or remove method overrides the program will still compile and run but unexpectedly do different things.

#### Parent and abstract classes must be unit tested too

They should be tested without the child classes. Abstract classes should have test implementations to be tested.


## What To Keep In Mind


#### Abstract classes and parent classes are *classes*

They must obey to everything what we expect from a class: They must be closed, complete, cohesive, tested and they must exactly do what their names tell.

#### Parent and child classes make *one polymorphic type*

Create parent classes only if you have one polymorphic type in mind. All parent and child classes in a hierarchy are in an "is a" relationship, so they are the same type.

Create parent classes if you really want/need to use it as a polymorphic type. E.g. for processing polymorphic instances in a collection.

#### Inheritance is the strongest *dependency*

We want to avoid any kind of dependencies because they multiply the complexity of the code and make its modification very hard. We should be careful when using the strongest dependency.

#### Occam's razor

Do not create code which is not necessary. Maintaining masses of unnecessary code needs a lot of efforts.

## Related posts

* [What Is The Problem With Inheritance?](http://petozoltan.github.io/2016/06/19/what-is-the-problem-with-inheritance.html)
