---
layout: post
title: "Clean Code Introduction"
date: 2016-08-24
---

This introduction does not go through the basics of the clean code. Instead of that it collects thoughts and advices for practicing  software developers.

***

* TOC
{:toc}

## Origin & Overview

### Uncle Bob & The Book

  - [Clean Code book cover](https://petozoltan.github.io/images/clean-code-outline/clean-code-book-cover.png)
  - [Uncle Bob, Robert C. Martin](https://d26o5k45lnmm4v.cloudfront.net/authors-robert-martin-v0.jpg)

### Named principles

- In the book: SRP, OCP, DIP, (IoC), DI, DRY, LOD, BSR, F.I.R.S.T.
- Not in the book: LSP, ISP, YAGNI, KISS, S.O.L.I.D.

Coding

  * **SRP** Single Responsibility Principle
  * **OCP** Open Closed Principle
  * **DIP** Dependency Inversion Principle
  * **(IoC)** Inversion of Control
  * **DI** Dependency Injection
  * **DRY** Don't Repeat Yourself
  * **LOD** Law of Demeter
  * **BSR** Boy Scout Rule
  * **LSP** Liskov Substitution Principle
  * **ISP** Interface Segregation Principle
  * **YAGNI** You Ain't Gonna Need It
  * **KISS** Keep It Simple Stupid
  * **S.O.L.I.D** SRP + OPC + LSP + ISP + DIP

Testing

  * **F.I.R.S.T.** Fast, Independent, Repeatable, Self-validating, Timely

### Why clean code?

- [The total cost of owning a mess](https://petozoltan.github.io/images/clean-code-outline/velocity-graph.png)
- [The real measure of code quality](https://petozoltan.github.io/images/clean-code-outline/code-quality-wtfs.png)

### What is bad code like?

Readability

- Spaghetti code
- Dependencies
- Fragile code
- Unreadable
- Mind mapping
- Duplication 
- Unexpected
- Magic numbers
- Overcomplexity
- Code smell
- Antipatterns
- Technical debt

Functionality

- Bugs
- Does not fulfill the specification
- Side effects

Programmer style

- Careless
- Sloppy
- Lazy
- Quick and dirty

### What is clean code like?

- Elegant
- Simple
- Direct
- Readable
- Expressive
- Carefully written
- Tested
- Bugs cannot hide
- Art

## Further Reading

- [Clean Code book, table of content](https://petozoltan.github.io/2016/08/19/clean-code-toc.html)
- [Effective Java book, table of content](https://petozoltan.github.io/2016/08/19/effective-java-toc.html)
- [Clean Code Big Outline](https://petozoltan.github.io/2016/08/19/clean-code-outline.html)
- [Clean Code Links](https://petozoltan.github.io/2016/08/20/clean-code-links.html)
- [Slideshows](http://www.slideshare.net/arturoherrero/clean-code-8036914)

## Advanced Thoughts

### What is clean code and what is it not?

Not code beautifying

- Code correctness

Not a set of mechanic rules

- Continuous thinking
- Half science, half art
  - continuous shaping the code
- Principles instead of rules
- Terms
- Violations are only 'code smells'

No numeric rules

- Only one numeric rule: it does 1 thing.
- 'Simple' instead of 'small'.

No boilerplate code templates

- Alway the best simplest direct solution

Not for code checkers

- Human readability, expressivity 

Not matter of taste

- Quest for an optimal implementation

Not waste of time

- Aims to finish the code
- Refactoring is not evil
- Technical debt is evil

Not easy

- Self discipline
  - it is easy to know the rules but not easy to apply them to ourselves 
  - easy to see other's bad code but not easy to recognize when we do them
- Long practice

### The ultimate goals of clean code

The software product should be...

- Error free
- Finished
- Maintainable

We realize the goals through...

- Expressiveness
- Granularity

### When is the code good?

If it is *decidable* whether it is good.

- It is a comparison
  - Specification vs. implementation
  - Declaration vs. definition
  - Names vs. code blocks {}

### Single Responsibility Principle

SRP is the core rule of clean code.

- [Good as it should be](https://petozoltan.github.io/images/clean-code-outline/single-responsibility-principle-1-ok.png)
- [Spaghetti code](https://petozoltan.github.io/images/clean-code-outline/single-responsibility-principle-2-spec.png)
- [Unwanted dependencies](https://petozoltan.github.io/images/clean-code-outline/single-responsibility-principle-3-impl.png)

### Reading the code with clean code view

I see independent, named code blocks { }:

- Does every code block {} do what its name tells?

  - Class's/Method's full declaration vs. definition block {}

- For one code block I do not care with anything else outside

  - No callers of the methods
  - No called methods from the given block
    - I check whether it depends on the called.

- For parent classes I don't care with the children

  - OCP, SRP, spaghetti

- Does everything have a name?

  - Methods: No inline implementation
  - Classes: No low cohesive classes

### Modifying the code with clean code view

Before modification

- Understand affected parts
- Check cleanness 
- If not clean, refactor

Do modification

- Change names first
- Implement code

## Typical Issues

### Refactoring

> "Refactor a little, code a little"

Before it was good:

``` java
getCustomers() {
    return dao.getCustomers();
}
```

After it is bad: Functionality changed, name not changed

``` java
getCustomers() {
    return dao.getCustomers(Status.ACTIVE);
}
```

Good: Name changed

``` java
getActiveCustomers() {
    return dao.getCustomers(Status.ACTIVE);
}
```

Good alternative: Declaration changed

``` java
getCustomers(Status status) {
    return dao.getCustomers(status);
}
```

### Readability

- It should be readable like "English prose".
- [It should be pseudo code.](https://petozoltan.github.io/2016/08/19/clean-code-outline.html#pseudo-code)

### Names

**Give names!**

- Method level: 
  - Methods instead of [inline implementations](https://petozoltan.github.io/2016/08/19/clean-code-outline.html#avoid-inline-implementation).
- Class level: 
  - More, small classes instead of big, [low cohesive classes](https://petozoltan.github.io/2016/08/19/clean-code-outline.html#does-more-things---low-cohesion).

**Naming struggle is a code smell!**

- If you cannot give a good name.
- Names like 'Abstract', 'Common', 'Base', etc. are not good.

### Duplication

**When general contains special**

Example: Bad: 'Almost the same' methods

``` java    
public ResultBean saveSomething(InputBean input) {

    logger.info("saveSomething started");
    ResultBean result = new ResultBean();

    ProgressDialog progress = new ProgressDialog(this);

    try {

        // Only this line is different
        Entity entity = SaveCustomer(input, progress);
        result.setEntity(entity);

    } catch (ValidationException e) {
        logger.error("Invalid input: " + input, e);
        throw new BusinessException(e);
    } catch (RuntimeException e) {
        logger.error("Unexpected error", e);
        throw e;
    } finally {
        listeners.sendEvent(SAVE_CUSTOMER_FINISHED);
        progress.close();
    }

    logger.info("saveSomething returned: " + result);
    return result;
}
```

``` java
public ResultBean saveSomething(InputBean input) {

    logger.info("saveSomething started");
    ResultBean result = new ResultBean();

    ProgressDialog progress = new ProgressDialog(this);

    try {

        // Only this line is different
        Entity entity = createIfNotExist(input, progress);
        result.setEntity(entity);

    } catch (ValidationException e) {
        logger.error("Invalid input: " + input, e);
        throw new BusinessException(e);
    } catch (RuntimeException e) {
        logger.error("Unexpected error", e);
        throw e;
    } finally {
        listeners.sendEvent(SAVE_CUSTOMER_FINISHED);
        progress.close();
    }

    logger.info("saveSomething returned: " + result);
    return result;
}
```

[How to refactor](https://petozoltan.github.io/images/clean-code-outline/refactoring-inline-implementation.png)

### Enums

- Use enums for constants
- Static information mapping
- [More...](https://petozoltan.github.io/2016/08/19/clean-code-outline.html#enums)

### Classes

**Tight cohesion**

- Single Responsibility Principle
- Members should use each-other
- [How to refactor](https://petozoltan.github.io/images/clean-code-outline/refactoring-low-cohesion.png)

**Loose coupling**

- [Dependency inversion](https://petozoltan.github.io/images/clean-code-outline/uml-dependency-inversion.png)

**Class types**

Service

- Stateless
- Private members
- Law of Demeter
- DI framework

Data

- No procedures
- New / ORM

**Inheritance**

Problems

- Hard to read, "mind mapping"
- The strongest dependency
- Misunderstanding of polymorphism
  - _A extends B_ reads _A is a B_
  - _A extends AbstractA_ reads _A is an AbstractA_
  - Names smell

Favor composition over inheritance 

_From the Effective Java book_

- Use inheritance only for real polymorphism
- Do not put common code into parent classes
  - Leads to low cohesion, SRP violation
- Composition:
  - Methods are the simplest dependency injection
  - Methods are the simplest abstraction
- Turn on warnings

Make methods final

_From the Effective Java book: Design and document for inheritance or else prohibit it_

- Overriding of implemented methods is forbidden
- Fragile code

Links

- [When to avoid inheritance?](https://petozoltan.github.io/2016/06/18/when-to-avoid-inheritance.html)

### Methods

**Avoid inline implementation**

- Methods doing more than one thing.
- This is unnamed functionality.

Bad: Method doing more than one thing (from the book)

``` java  
// It does three things
public void pay() {
    for (Employee e : employees) {
        if (e.isPayday()) {
            Money pay = e.calculatePay();
            e.deliverPay(pay);
        }
    }
}
```
  
Good: Methods doing one thing (from the book)

``` java  
public void pay() {
    for (Employee e : employees) {
        payIfNecessary(e);
    }
}

private void payIfNecessary(Employee e) {
    if (e.isPayday()) {
        calculateAndDeliverPay(e);
    }
}

private void calculateAndDeliverPay(Employee e) {
    Money pay = e.calculatePay();
    e.deliverPay(pay);
}
```
 
**Do not return null**

**Do not explicitly pass null**

**Overload methods only if they do the same**

- They physically call the same method
- Only for convenience methods with different parameters

**Do not mix two types of methods**

- Coordinator, "logic"
- Technical

**No side effects**

Take care of invisible side effects

- Transactions
- Concurrency

**Avoid never-ending method chain**

``` java
save() {
    doSomething();
    doSomething();
    doSomething();
    doTheSave();
}

doTheSave() {
    doSomething();
    doSomething();
    doSomething();
    doReallyTheSave();
}

doReallyTheSave() {
    doSomething();
    doSomething();
    doSomething();
    nowItComesToTheSave();
}

// etc.
```

### Programmers 

- Always ask whether the code does what it should do by the names
- Read back your code
- Check clean code principles
- Avoid workaround programming - against our own code
- Stop & think if too complicated

### Unit test

- Strictly belongs to clean code.
  - Helps to finish the code units.
- Helps to modify the code: Regressions tests.
- Write unit tests instead of debugging.
- Helps to write testable code.
  - Methods with clear and direct input and output.

### Warnings

- Do not commit warnings!
- Do not hide IDE warnings!
- Do not suppress warnings!

### Other antipatterns

**Do not write 'handleError()' methods**

- They does not express the program flow (exception?)
- They cheat the compiler too (unreachable code)
- Instead create a method with return value 

Bad: What will happen? What does it do? What information is used?

``` java
    } catch(Exception e) {
        handleException(e);
    }
```

Good: It is clear

``` java
    } catch(Exception e) {
        throw createServiceException(e, ...);
    }
```
