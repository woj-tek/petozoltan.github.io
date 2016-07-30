## Avoid constant collection classes

Programmers often create separate classes to store constants of a certain area, "to have them at one place" or "to avoid polluting" the procedural classes. But it is not enough to make the code clean. What is the problem with them and how can we solve it?

#### Interpretation problems

When new constants have to be created it is not mandatory to add them to the collection class. Developers can decide to add constants to the collection or to create them somewhere else. Unfortunately this is another problem that makes OOP very hard:

> If it is not obvious where to write the new code then the chaos begins...

#### Classes should not always be extended

Think on the _Open/Closed Principle_. Classes should be closed for modification. At a certain point a class must be tested and finished, in order to have a reliable code. But constant collections are loose and generic, so they are like never finished. When you look at such a class, you cannot decide whether it is finished or not.

#### Prefer enums to constants

In most cases it is better to use enums instead of constants. Enums have more benefits over constants:

* Enums define and limit a specific _value set_. So it is clear to which enum a new value has to be added.
* They are type safe.
  Example:.First names and last names are not assigneable, but if both are Strings they can be assigned to each-other. With enums it is not possible.
* They can be provided with additional useful information too.
  Example: A message box title and content can be implemented with two constants but with one enum.
  
#### Split into more enums

Usually a constant collection should be split into more than one enums. You can see a clear sign for that in the following cases:

* The constants have different types.
* The constants' names begin with different _prefixes_ .
* Constants are grouped by comments.

#### Example

