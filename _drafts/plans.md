## Avoid constant collection classes

* Interpretation problems. 

  > It can be this way or that way. Wrong.
  
  New constants can be added to this class or to separate classes. 
  If the next developer cannot decide where to write the code, the chaos begins.

* Classes should be specific

* Constants should always be enums.

  Enums of one specific value set. (E.g. first names and last names are both Strings, but the _value set of first names_ and the _values set of last names_ are not assignible.)
  
  They can be provided with additional information.
 
