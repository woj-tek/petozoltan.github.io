## Avoid constant collection classes

#### Interpretation problems. 

> It can be this way or that way. It is a matter of taste.
  
Wrong. New constants can be added to this class or to separate classes. 
If the next developer cannot decide where to write the code, the chaos begins.

#### Classes should be specific

That's what they are for. 
Think on _high cohesion_ or the _Single Responsibility Principle_.
Classes should be closed for the contiuous modifications. A class should be implemented and unit tested, and _finished_. Modifications should rather go in new classes than in existing ones.

#### Constants should always be enums.

Enums of one specific value set. (E.g. first names and last names are both Strings, but the _value set of first names_ and the _values set of last names_ are not assignible.)
  
They can be provided with additional information.
  
#### Prefixes in constant names

When you see _prefixes_ in the constants' names, that is a clear sing that the constant set should be split into more enums.
