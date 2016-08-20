---
layout: post
title: "Clean Code Outline"
date: 2016-08-19
---

***

* TOC
{:toc}

***

![](https://petozoltan.github.io/images/clean-code-outline/clean-code-book-cover.png)

## Why Clean Code?

### Enterprise Software

It is not enough to learn a programming language. We have to develop enterprise software which are:

* Large: 100k – 1M lines
* Long life cycle (years)
* Complex
* Many developer
* Many modifications
* Iterative development

### Problems

* Many bugs - potential bugs hiding in the code
* Code is too complex - hard to understand
* Code is fragile - changes causes new bugs, side effects
* Falling productivity - low development speed
* Unreliable, impossible estimations
* Too much Technical Debt collected

### Technical Debt

* Invisible
* "Should have been done"
* "We will fix it later"
* Result of "quick & dirty" coding
* Poorly written code is a technical debt - _"Should be written better"_

![](https://petozoltan.github.io/images/clean-code-outline/velocity-graph.png)

> Technical debt is the biggest risk of the development

## Clean Code

### Expectations

* The code should show what is does
* The code should show the intentions of its programmer - _Express what you will_
* The code should reflect the specification - _Business analysts should be able to see the business algorithms in the code_
* Reviewers should be able to decide whether the code is good or not
* Logical
* Direct, straightforward
* Reduce cost and risk of changes
* Good, correct
* Less bugs
* Code quality

> The main goal is to see that the code correctly does what the specification requires

### Goals

* Readable - _We spend much more time with reading than with writing._
* Understandable
* Simple
* Effective
* Easy to change - _Not "fragile"_
* Testable
* Fragmented
* Reliable
* Intentional
* Mirrors what it does
* Does what it is expected to do - _No unexpected solutions_
* Complies with known patterns
* Clean from „dirt” and pollution - _Boy Scout Rule: Leave it clean_
* Error free - _Makes hard for bugs to hide_

### Main Rules

* One code part implements one thing - _block, method, class, package, compilation unit_
* Implement things in a correct part - _misplaced responsibility_
* Meaningful names (business meaning)
* No magic numbers (and strings and booleans)
* No code repetition - _One thing is implemented once, one information is written once_
* Expected behavior
  * "Least astonishment"
  * Count of WTFs :-)
  * No arbitrary solutions
  * Use known conventions and patterns

> Clean code = Expressiveness + modularity

### Code Quality

#### Possible Measurements

There is no overall and ultimate measure of code quality.

* Number of warnings
* Static code checkers - _CheckStyle, FindBugs, PMD, Sonar, ..._
* Complexity - _Cyclomatic complexity_
* Code smell
* Unit test coverage

![](https://petozoltan.github.io/images/clean-code-outline/code-quality-wtfs.png)

### Developer Precisity

* Be precise
* Think
* Do not be careless
* Do not be arbitrary
* Be consequent

### Code Smell

* The feeling that something is not yet good with the code

### Issues

#### Avoid dogmatic style

* Always interfaces
* Always accessors/mutators (getters/setters)
* Structured programming: Only one return
* Mandatory comments -no comments needed for private methods

Example: Bad: Dogmatic style

``` java
// Dogmatic comment results obvious comment
// Dogmatic getters/setters

/**
* Getter of {@link #_inputSource}.
* @return {@link #_inputSource}
*/
public final InputSource getInputSource() {
    return _inputSource;
}

public final void parse(final String[] configs, final String configPath, final boolean flushAfterParse) {
    if (getInputSource() != null) { }
}
```

## Clean Code Approaches

### Simple Design / Emergent design

Author: _Kent Beck_

* Runs all the tests
* Contains no duplication
* Expresses the intent of the programmer
* Minimizes the number of classes and methods

### Pseudo code

* The code should look like a pseudo code
* The types and methods and names we create are pseudo code really
* DSL - Domain Specific Language
* The business analyst should be able to understand it

Example: Pseudo code

```
"Take the higher prices":

if Master prices are higher than in Increase then
   apply Master prices to the Increase
and
   apply Master conditions to the Increase
if Master discount fare is higher than in Increase then
   apply Master discount fare to the Increase
```

Example: Good: Java code

``` java
void compareAndUpdateIncrease(PricingResponseDTO masterResponse, PricingResponsePaxfares masterPaxFares, 
        PricingResponseDTO increaseResponse, PricingResponsePaxfares increasePaxFares) {
    
    if (isMasterPriceHigherOrEqual(masterPaxFares, increasePaxFares)) {
        updateIncreasePrices(masterPaxFares, increasePaxFares);
        updateIncreaseConditions(masterResponse, increaseResponse);
    }

    if (isMasterMaxDiscountFareHigher(masterPaxFares, increasePaxFares)) {
        updateIncreaseMaxDiscountFares(masterPaxFares, increasePaxFares);
    }
}
```

Example: Change request

```
"Always take the conditions from the master."
```

Example: Good: Changed code

``` java
void compareAndUpdateIncrease(PricingResponseDTO masterResponse, PricingResponsePaxfares masterPaxFares, 
        PricingResponseDTO increaseResponse, PricingResponsePaxfares increasePaxFares) {

    if (isMasterPriceHigherOrEqual(masterPaxFares, increasePaxFares)) {
        updateIncreasePrices(masterPaxFares, increasePaxFares);
    }
    
    updateIncreaseConditions(masterResponse, increaseResponse);
    
    if (isMasterMaxDiscountFareHigher(masterPaxFares, increasePaxFares)) {
        updateIncreaseMaxDiscountFares(masterPaxFares, increasePaxFares);
    }
}
```

### Specification vs. Implementation

* Specification: Name or description or "contract" or "promise" = _class and method declarations_
* Implementation: "internal part" that fulfills the promise = _code block {}, package content, etc._
* Every code unit is a "separate world" - _e.g. class or method blocks_

### What does this code do?

* The reader will ask it
* The developer should ask it

### Metric Rules

* There are NO numeric rules like maximum lines of code, number of parameters, level of indentation, etc.
* The only numeric rule is: One code does one thing + One thing is implemented once
* Classes and methods should be "small" but it is not exactly defined

### Developers

* Do not only satisfy the compiler or the unit tests
* Be the reader of your own code - _stop and think_
* "Tell the story" with proper types and names
* Describe the business logic with English words as much as possible

### Avoid "Enemies" of the Code

* No duplication - _DRY_
* No inline implementation
* No misplaced code
* No parallel development - _"spaghetti code"_
* No unused code - _"dead code"_

### Clean Code is an Art

* Not a set of mechanical rules
* More principles to apply
* Continuous thinking and shaping the code - _"step back"_

### Scrum

* "Code is clean"' should be part of Definition of Done

## Specification & Design

Everything starts with this. But if it is not understood well, the clean coding is worth for nothing.

### Specification

* Specification must be clear, complete and consistent
* Specification must be well understood by the developers
* Avoid implementing a poorly specified features - _they will ruin the code_

### Design

#### Do not underdesign

* The design should be a correct and complete solution for the given problem
* Draw examples to see every possible cases and to find the good solution

#### Do not overdesign

* Do not design for assumptions
* Do not design solutions which will be used much later - _"They will be good in the future"_
* YAGNI - _You Ain't Gonna Need It_

## No Duplication

One of the "enemies" of clean code.

### Cases of duplication

* Copy-pasted parts
* Duplicated logic - _something implemented more times on different ways_
* Duplicated values or information - _literals or constants_

### Avoid inline implementation

This is also a _misplaced responsibility_!

* Not reusable - Leads to duplication
* Different implementations
* Not testable
* Refactor it

### DRY Principle

* Don't repeat yourself (Kent Beck)

Example: Refactor inline implementation

![](https://petozoltan.github.io/images/clean-code-outline/refactoring-inline-implementation.png)

Example: Bad: Duplication causes incorrect intention

``` java
// It suggests that it is a branching, but it is only a duplicate
// It differs only in the input value, which is implemented inline

public boolean isMultipleOriginAllowedForCountry(SearchFlightsForm form) {
    if (GstUserType.INTERNAL == userHelper.getCurrentUserUserType()) {
        return isCountryInTheListOfAllowedMultipleOrigins(form.getPos().getCode());
    } else {
        return isCountryInTheListOfAllowedMultipleOrigins(userHelper.getCurrentUserPos());
    }
}
```

Example: Good: No duplicates, correct intention

``` java
public boolean isMultipleOriginAllowedForCountry(SearchFlightsForm form) {
    return isCountryInTheListOfAllowedMultipleOrigins(getPosOfUser(form));
}

// Extracted funtionality can be tested too
private String getPosOfUser(SearchFlightsForm form) {
    return GstUserType.INTERNAL == userHelper.getCurrentUserUserType() ? 
            form.getPos().getCode() : userHelper.getCurrentUserPos();
}
```

Example: Bad: Duplicated implementation with differences

``` java
// Cause: laziness of the developer
// Cannot be found by a code checker
// Blocks the development and the refactoring too

public final void parse(final String[] configs, final String configPath, final boolean flushAfterParse) {
    final FileLocator locator = new FileLocator();
    try {
        if (getInputSource() != null) {
            final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
            final String extendedConfigPath = StringUtils.isEmpty(configPath) ? "" : configPath + CharacterConstant.SLASH;
            for (final String config : configs) {
                final File grammarFile = locator.locate(extendedConfigPath + config + ".xml");
                parser.addConfig(new Config(config, grammarFile));
            }
            parser.convert();
            if (flushAfterParse) {
                getHandler().flush(true);
            }
        }
    } catch (final IOException e) {
        throw new ExtendedRuntimeException(e);
    } catch (final ExtendedException e) {
        throw new ExtendedRuntimeException(e);
    } finally {
        locator.releaseAll();
    }
}

public final void parse(final Config[] configs, final boolean flushAfterParse) {
    final FileLocator locator = new FileLocator();
    try {
        if (getInputSource() != null) {
            final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
            for (final Config config : configs) {
                parser.addConfig(config);
            }
            parser.convert();
            if (flushAfterParse) {
                getHandler().flush(true);
            }
        }
    } catch (final IOException e) {
        throw new ExtendedRuntimeException(e);
    } catch (final ExtendedException e) {
        throw new ExtendedRuntimeException(e);
    } finally {
        locator.releaseAll();
    }
}

// Other clean code issues in this example:
// - Methods are doing more than one thing
// - Inner dependency
// - Not expressive validity check
```

Example: Bad: Duplicates differ only in values

``` java
// Bad intention: similar methods with very different names - how can be that?
// Methods do what they tell but you CANNOT SEE it
// It contains another duplication which can be expensive (e.g. database access)

private void fillOutCountriesForMultipleOrigin() {
    getSegments().get(0).setOrigin(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
    }
}

private void removeCountriesForNormalFlights() {
    getSegments().get(0).setOrigin(null);
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(null);
    }
}
```

Example: Good: Refactor value differences to input parameters

``` java
// Methods do what they tell and you CAN SEE it

private void fillOutCountriesForMultipleOrigin() {
    setCountryForSegments(countryAutoCompleteHelper.getCountryItemForAiportCode(getPosForMultipleOrigin()));
}

private void removeCountriesForNormalFlights() {
    setCountryForSegments(null);
}

private void setCountryForSegments(AirportCityCodeItem country) {
    getSegments().get(0).setOrigin(country);
    if (JourneyType.OPEN_JAW.equals(getJourneyType())) {
        getSegments().get(1).setDestination(country);
    }
}

// It is not yet clean: magic numbers
// It is not yet clean: why only two segments?
```

## Refinement & Refactoring

### Successive Refinement

* Write a draft or "monolith" first
* Refine/refactor it

### Coding Cycle

* Think
* Code
* Think again
* Optimize/refactor

### Modifications

* Refactor first, write code after that
* Change the "pseudo code" first, the real code after that
* Refactor to isolate changed part

### Refactoring

* Refactoring is good, technical debt is bad
* Refactoring is a mandatory part of the iterative development
* Continuously refactor unclean code to clean code
* Always refactor for changes in the requirements - _"Until now the program had to do this, from now on the program has to do that"_

### Design Patterns

(Not part of this training. See links.)

> Perfection is achieved, not when there is nothing left to add, but when there is nothing left to remove. (Antoine de Saint-Exupery)

## Conventions

* Language conventions - _Java Code Conventions (Sun, 1997)_
* International conventions, design patterns - _Software Design Patterns_
* Project's coding conventions

## Names

### Rules

* Meaningful
* Intentional - _telling what it does_
* Readable, understandable
* Self-explanatory
* Not disinforming
* Pronounceable
* Consequent
* Do not force 'mind-mapping'

### Practice

* Names just repeat the types - _if types are correct and methods are small_
* The same object should have the same name when passed to other methods - _not always but usually_
* Prefer positive conditional names - e.g. avoid !isNot()_

### Some conventions

* Class name: noun
* Method name: verb
* Avoid prefixes and technical terms (e.g. Abstract)
* Name length corresponds scope length
* Old Enterprise JavaBeans - EJB
* Comply with: Java Code Conventions (Sun, 1997)

### EJB - Enterprise JavaBeans

* `private Foo foo` - _foo is a 'property' name_
* `public Foo getFoo()` - _the property name with a capital_
* `public void setFoo(Foo foo)`
* `public boolean isSomething()` - _also hasSomething()_

Example: Bad: Names

``` java
class DtaRcrd102 {

    // Not meaningful, not readable, not pronounceable
    Date genymdhms;
    Date modymdhms;
    String pszqint = "102";

    // Avoid prefixes and Hungarian notation
    String m_dsc;
    String strName;

    // Hard to read
    XYZControllerForEfficientStorageOfStrings con1;
    XYZControllerForEfficientHandlingOfStrings con2;

    // Disinforming
    void setName(String name) {
        m_dsc = name;
    }

    // Not informative
    void doCalculation() {

        // Too short names, Magic numbers
        for (int j=0; j<34; j++) {
            s += (t[j]*4)/5;
        }
    }
}
```

Example: Good: Names

``` java
class Customer {

    private String description;
    private Date generationTimestamp;
    private Date modificationTimestamp;;
    private final String recordId = "102";
    int realDaysPerIdealDay = 4;
    const int WORK_DAYS_PER_WEEK = 5;
    int sum = 0;

    void setDescription(String description) {
        this.description = description;
    }

    int calculateWeeks() {
        for (int j=0; j < NUMBER_OF_TASKS; j++) {
            int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
            int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
            sum += realTaskWeeks;
        }
        return sum;
    }
}
```

Example: Bad: Not informative names

``` java
// What does it really do?
assertThat(scores, is(StudentService.collectScores(STUDENT_LIST2)));
```

Example: Good: Informative names

``` java 
// Readable: "It creates an empty score list from an empty student list"
assertThat(emptyScoreList, is(StudentService.collectScores(STUDENT_LIST_EMPTY)));
```

Example: Bad: Not informative name of input parameter

``` java
// What kind of input value is converted?
// It is not a 'find' but rather a 'convert'
private String findDeadlineType(int i) {
    String result;
    switch (i) {
    case 0:
        result = RK_FIRST_NAME_DEADLINE;
        break;
    case 1:
        result = RK_SECOND_NAME_DEADLINE;
        break;
    default:
        result = ""; //future values come here
        break;
    }
    return result;
}

// Best practice: Refactor to enum
```

Example: Bad: Confusing characters _(From the book)_

``` java
    int a = l;
    if ( O == l )
        a = O1;
    else
        l = 01;
```

Example: Good: Name lengths correspond to scope

``` java
// The class is one screen long
@Component
public class NameDeadlineReminderMessageCollector {

    @Autowired
    private DeadlineReminderMessagePnrFilter filter; // Used only in this class

    @Autowired
    private DeadlineReminderMessageSorter sorter; // Used only in this class

    @Transactional(readOnly = true)
    public List<DeadlineReminderMessage> collectDeadlineRemindersByAgency(String agencyInternalId) {
        return sorter.sort(filter.filter(findDeadlines(agencyInternalId), findPnrs(agencyInternalId)));
    }
    
    @Transactional(readOnly = true)
    public List<DeadlineReminderMessage> collectDeadlineRemindersByPoses(List<String> poses) {
        return sorter.sort(filter.filter(findDeadlines(poses), findPnrs(poses)));
    }
}
```

## Types

> The goal of typed languages is to pull issues from run time to compile time.

### Rules

* Use types
* Do not use String for non-textual values
* Do not use Strings for dates - _it is always formatted!_
* Avoid using boolean parameters - _hard to read, "magic numbers"_
* Create exception types instead of error codes

### Enums

* Enums are static constants
* You can static import enums to shorten the code
* Enums are created threadsafe
* Always use enums for a finit set of constants
* Use enum to map information
* Prefer enums to maps
* Prefer enums to switches
* Enums cannot have a parent class but can implement interfaces

Example: Bad: Implementation with collections and procedures

``` java
public final class ContractFormatter implements Serializable {
    
    // They belong to formatFareFamily(), low cohesion
    // Misplaced constants
    // Duplications: they are defined sever times again and again...
    private static final String FORMATTED_FIRST_CLASS_FAM = "First";
    private static final String FORMATTED_BUSINESS_FAM = "Business";
    private static final String FORMATTED_ECONOMY_FAM = "Economy";
    private static final String FIRST_FAM = "FIRST";
    private static final String BUSINESS_FAM = "BUSINESS";
    private static final String ECONOMY_FAM = "ECONOMY";
    private static final String FORMATTED_ECONOMY_SAVER_FAM = "Economy Saver";
    private static final String ECOSAVER_FAM = "ECOSAVER";
    private static final String LIGHT_FB = "LIGHT_BUNDLE";
    private static final String CLASSIC_FB = "CLASSIC_BUNDLE";
    private static final String BUSINESS_FB = "BUSINESS_BUNDLE"; //FB_TODO: chage to final name
    private static final String FORMATTED_LIGHT_FB = "Light";
    private static final String FORMATTED_CLASSIC_FB = "Classic";
    private static final String FORMATTED_BUSINESS_FB = "Business"; //FB_TODO: chage to final name
    
    // Simple property implemented as a collection
    // It belongs to isFareBundle(), low cohesion
    private static final Set<String> fareBundleStrings = ImmutableSet.of(LIGHT_FB, CLASSIC_FB, BUSINESS_FB);
    
    public boolean isFareBundle(String famOrBundle) {
        return fareBundleStrings.contains(famOrBundle);
    }
    
    // Simple mapping implemented as a procedure
    public String formatFareFamily(String famOrBundle) {
        String fareFamily = famOrBundle;
        switch (famOrBundle) {
        case ECOSAVER_FAM:
            fareFamily = FORMATTED_ECONOMY_SAVER_FAM;
            break;
        case ECONOMY_FAM:
            fareFamily = FORMATTED_ECONOMY_FAM;
            break;
        case BUSINESS_FAM:
            fareFamily = FORMATTED_BUSINESS_FAM;
            break;
        case FIRST_FAM:
            fareFamily = FORMATTED_FIRST_CLASS_FAM;
            break;
        case LIGHT_FB:
            fareFamily = FORMATTED_LIGHT_FB;
            break;
        case CLASSIC_FB:
            fareFamily = FORMATTED_CLASSIC_FB;
            break;
        case BUSINESS_FB:
            fareFamily = FORMATTED_BUSINESS_FB;
            break;
        default:
            break;
        }
        return fareFamily;
    }
}
```

Example: Good: Information and mapping as enum

``` java
import static com.lhsystems.sales.gst.common.domain.FareCategory.*;

public enum FareCode {
        
    ECOSAVER(FAMILY, "Economy Saver"),
    ECONOMY(FAMILY, "Economy"),
    BUSINESS(FAMILY, "Business"),
    LIGHT_BUNDLE(BUNDLE, "Light"),
    CLASSIC_BUNDLE(BUNDLE, "Classic"),
    BUSINESS_BUNDLE(BUNDLE, "Business"),
    FIRST(CLASS, "First");

    private FareCategory category; // Property
    private String displayInContract; // Mapping to another information
    
    private FareCode(FareCategory category, String displayInContract) {
        this.category = category;
        this.display = display;
    }
    
    public String getDisplay() {
        return display;
    }
    
    private boolean isFareBundle() {
        return category == BUNDLE;
    }
}
```

### Smells

* Do not pass parameters in a map

Example: Bad: Parameter map

``` java 
// Unintentional
// Shifts program errors to run time

void someMethod() {
    Map<String, Object> parameters = new HashMap<>();
    parameters.put("contract", contract);
    parameters.put("requestNr", 1);
    parameters.put("userId", user.getId());
    otherMethod(parameters);
}

void otherMethod(Map<String, Object> parameters) {
    Contract contract = (Contract) parameters.get("contract");
    Integer requestNr = (Integer) parameters.get("requestNr");
    Long userId = (Long) parameters.get("userId");
    ...
}
```

> Everything should be made as simple as possible, but not simpler. (Albert Einstein)

## Methods

### Rules

* "Small" - _Not an exact rule_
* Do only one thing - _even small methods may do more things!_
* One level of abstraction - _See Law of Demeter later_
* No unexpected behavior (side effects)
* No unexpected or not-understandable input and return values
* No or the least possible dependencies
* Avoid inline implementation - _put it always in a separate method_
* Set visibility modifiers precisely - _For the compiler and for the reader too_
* Check parameter validity at the beginning - _Item 38 in Effective Java (2nd Edition, Joshua Bloch, 2008)_
* Prevent overriding non-abstract methods - _Item 17 in Effective Java (2nd Edition, Joshua Bloch, 2008)_

Example: Bad: Unexpected behavior

``` java
boolean checkPassword(String pwd) {
    if( pwd.equals(„secret”) ){
        createSession(); // Unexpected side effect
        return true;
    } else {
        return false;
    }
}
```

Example: Bad: Unintentional return values

``` java
    int createProcess();

    // Which one is correct?
    errorCode = createProcess()
    processNumber = createProcess()
    processCount = createProcess()
    createdInMillis = createProcess()
```

Example: Bad: Method doing more than one thing

``` java
// Are the lines in the proper order?
public synchronized void flush() throws IOException {
    getContentBuffer().flush();
    IOUtils.copy(new StringReader(getContentBuffer().getBuffer().toString()), getBufferedWriter());
    getBufferedWriter().flush();
    contentBuffer = new StringWriter();
}
```

Example: Good: Methods doing one thing

``` java
// Method complies with the contract
@Override // This is also important, not only for the compiler
public synchronized void flush() throws IOException {
    flushMyBuffer();
    getBufferedWriter().flush();
}

private synchronized void flushMyBuffer() throws IOException {
    contentBuffer.flush();
    IOUtils.copy(new StringReader(getContentBuffer().getBuffer().toString()), getBufferedWriter());
    contentBuffer = new StringWriter();
}

// Now it is clear that it has two buffers. Is is a good solution?
// Clean code is not the final goal, it is a way to the goal:
// is the code correct?
```

Example: Bad: Method doing more than one thing _(from the book)_

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

Example: Good: Methods doing one thing (from the book)

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

Example: Bad: Side effect: modifying the input parameter

``` java
// Incorrect name
private SelectedDirectionDTO createSelectedOption(OptionDTO option, String fareFamily) {

    SelectedDirectionDTO so = new SelectedDirectionDTO();
    so.setId(option.getId());
    so.setOrigin(option.getOrigin());
    so.setOriginCountry(option.getOrginCountry());
    so.setDestination(option.getDestination());
    so.setDepartureDate(option.getDepartureDate());
    so.setDepartureTime(option.getDepartureTime());
    so.setArrivalDate(option.getArrivalDate());
    so.setArrivalTime(option.getArrivalTime());
    so.setMultipleOrigin(option.isMultipleOrigin());
    so.getFlights().addAll(option.getFlights());

    // Non-standard TODO comment
    // Not informative comment
    //FB_TODO: the code from here might need changes
    // Negative condition first: harder to understand
    if (!moreOptions) {
        // Inline implementation
        for (RoutingFareDTO cFare : option.getFares()) {
            if (routingFareMatches(fareFamily, cFare)) {
                so.setFare(cFare);
            }
        }
    } else {
        // Inline implementation
        String fam = famMoreOptionMapping.get(fareFamily);
        if (fam != null) {
            for (RoutingFareDTO fare : option.getFares()) {
                if (fam.equalsIgnoreCase(fare.getCompartment())) {
                    so.setFare(fare);
                    // Modifying the input parameter!
                    so.getFare().setFareFamily(fareFamily);
                }
            }
        }
    }
    return so;
}
```

### Avoid Bad Input Parameter Types

* Object
* String for non-textual types
* boolean for switches - _use constants or enum instead_

### Program to Methods

Stateless, independent methods:

* Prefer return values to modifying input variables
* Prefer methods that depend only on the input parameters -No configuration parameters or data mining inside
* Independent = easily testable

At the end of the method calls there should always be a method that depend only on the input parameter and whose only result is the return value (or exception).

### Overloading

* Use overloading only for convenience
* For example for default values
* Do not use it for hiding differences
* They should call each other - _code smell if they don't_

### Hiding

* Hide irrelevant details in a separate method
* Do not hide relevant details in a separate method

Example: Bad: Overloads and Hiding

``` java
// Overloads doing different things
// relevant details are hidden (what lists are created)
List<Integer> scores = initScores(10, 0);
List<Integer> scores = initScores(10);
```

Example: Good: No overloads and Hiding

``` java
// Method intention is expressed in their names
// only irrelevant details are hidden (how lists are created)
List<Integer> scores = createListWithEqualNumbers(10, 0);
List<Integer> scores = createListWithDifferentNumbers(10);
```

### Two types of methods

* "Coordinator" or "orchestrator"
* "Technical" or "Algorithm"

Example: Good: Types of methods

``` java
// Orchestrator method - Easy to read - Business logic
public void modifySomething(Something s) {
    s.setAnything( s.getThis(), s.getThat() );
    if( s.isBig() ) {
        s.setSomethingElse( DEFAULT_SOMETHING_ELSE );
    }
}

// Algorithm method - Easy to test
public Anything calculateAnything(This this, That that) {
    return this.getCount() * that.getSize();
}
```

How to use these types:

* Do not mix business lines with technical lines
* Do not pollute the code with technical details
* Hide irrelevant details
* Do not hide relevant details

Example: Bad: Pollution by repeating irrelevant technical details

``` java
@Override
public List<DeadlineReminderMessageDTO> loadOptionDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.OPTION_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}

@Override
public List<DeadlineReminderMessageDTO> loadNameDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.NAME_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(), 
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}

@Override
public List<DeadlineReminderMessageDTO> loadTicketingDeadlineRemindersByPoses(List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + SpsRestEndpoint.TICKETING_DEADLINE_REMINDERS_GD.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}
```

Example: Good: No repeating technical details

``` java
import static com.lhsystems.sales.gst.services.spsaccessor.rest.SpsRestEndpoint.*;

@Override
public List<DeadlineReminderMessageDTO> loadOptionDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(OPTION_DEADLINE_REMINDERS_GD, gdUserPoses);
}

@Override
public List<DeadlineReminderMessageDTO> loadNameDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(NAME_DEADLINE_REMINDERS_GD, gdUserPoses);
}

@Override
public List<DeadlineReminderMessageDTO> loadTicketingDeadlineRemindersByPoses(List<String> gdUserPoses) {
    return loadDeadlineRemindersByPoses(TICKETING_DEADLINE_REMINDERS_GD, gdUserPoses);
}

private List<DeadlineReminderMessageDTO> loadDeadlineRemindersByPoses(SpsRestEndpoint endpoint, List<String> gdUserPoses) {
    UriComponentsBuilder componentsBuilder = UriComponentsBuilder.fromHttpUrl(GSP_ROOT_URI + endpoint.getValue());
    componentsBuilder.queryParam("gdUserPoses", gdUserPoses.toArray());
    return loadDeadlineReminderMessages(componentsBuilder);
}

private List<DeadlineReminderMessageDTO> loadDeadlineReminderMessages(UriComponentsBuilder componentsBuilder) {
    ResponseEntity<List<DeadlineReminderMessageDTO>> responseEntity = restTemplate.exchange(
            componentsBuilder.build().toString(),
            HttpMethod.GET, 
            null, 
            new ParameterizedTypeReference<List<DeadlineReminderMessageDTO>>() {}, 
            Collections.emptyMap());
    return responseEntity.getBody();
}
```

### Smells

* Passing this to a method -it could be implemented with more, smaller and readable classes.

> If you can mix a method's lines and it still compiles, it probably does more things. (Zoltan Peto :-)

## Nulls and Validity Checks

### Avoid NullPointerExceptions (NPE)

* Check at the beginning - _Unhappy path, Happy path_
* Consider using helper methods
* Check each object which is de-referenced in the method - and only these ones

Example: Bad: Null check at the wrong place

``` java
void doSomething(MyClass input) {
    if(input != null) { // Unnecessary here
        doStuff(input);
    }
}

void doStuff(MyClass input) {
    input.setData(10); // Would be necessary here
}
```

Example: Good: Null check always and only when dereferencing

``` java
void doSomething(MyClass input) {
    doStuff(input);
}

void doStuff(MyClass input) {
    if(input == null) {
        return;
    }
    input.setData(10);
}
```

### Defensive Programming

Also known as Secure Programming. A larger topic, but some elements:

#### Inputs

* Never trust data coming from outside - _user input, external systems_
* Fail early, Fail clean
* Create and use immutable types

#### Outputs

* Do not modify a data through getters
* Prevent it if possible - _unmodifiable collections_
* Create and use immutable types

Example: Bad: Unclear validity check

``` java
// What to do when input source is null?
// Why is the entire content indented?
public final void parse(final Config[] configs, final boolean flushAfterParse) {
    if (getInputSource() != null) {
        final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
        for (final Config config : configs) {
            parser.addConfig(config);
        }
        parser.convert();
        if (flushAfterParse) {
            getHandler().flush(true);
        }
    }
}
```

Example: Good: Validity check at the beginning

``` java
public final void parse(final Config[] configs, final boolean flushAfterParse) {
    // Unhappy path
    if (getInputSource() == null) {
        return; // Do nothing, return default or throw exception
    }
    // Happy path or Normal flow
    final EdifactParser parser = new EdifactParser(getInputSource(), getHandler());
    for (final Config config : configs) {
        parser.addConfig(config);
    }
    parser.convert();
    if (flushAfterParse) {
        getHandler().flush(true);
    }
}
```

### Parameters

* Do not pass explicitly null - _it is a "cheating", _allow it with an overloaded method_

### Unit Test of Inputs

* Unit test will nulls and empty values in all possible ways
  * null object
  * entire collection or array is null
  * collection or array element is null

### Error Handling

* Do not return null - _rather throw exception_

> Things must not be multiplied beyond necessity. The simplest solution is the best. (Occam’s Razor)

## Comments

### Write the least possible comments

* Prefer coding to commenting
* The code should document itself as most as possible
* Many and long comments are code smell

### Comments Should Be

* Meaningful
* Necessary
* Readable

### Bad Comments

* „Commented out” code - _Remove it, find it in the version control system_
* Separators, markers
* Redundant
* Misleading
* Out-of-date
* Obvious
* Unnecessary
* Funny
* Closing brace comment
* Attributes - _author, date, issue number, etc._
* Non-English
* Too many HTML markers
* Historical
* Prone to copy-paste error

### Good Comments

* TODO comments
* Warnings - _e.g. "Not threadsafe"_
* Limitations - _e.g. "It works only with a sorted list"_
* Javadoc comment to public API - _for high level service methods_
* Comment empty blocks
* Less is more.

Example: Bad: Comments

``` java
// Redundant, obvious:
/**
* gets the value of Name
*/
public String getName();

// Funny, unnecessary:
// I invented this part, but do not know why
```

Example: Good: Javadoc comment

``` java
/**
* Returns an Image object that can then be painted on the screen.
* The url argument must specify an absolute {@link URL}. The name
* argument is a specifier that is relative to the url argument.
* <p>
* This method always returns immediately, whether or not the
* image exists. When this applet attempts to draw the image on
* the screen, the data will be loaded. The graphics primitives
* that draw the image will incrementally paint on the screen.
*
* @param url an absolute URL giving the base location of the image
* @param name the location of the image, relative to the url argument
* @return the image at the specified URL
* @see Image
*
* @deprecated Use {@link getImage(Long id)} instead.
*/
@Deprecated
public Image getImage(URL url, String name) {
    try {
        return getImage(new URL(url, name));
    } catch (MalformedURLException e) {
        return null;
    }
}
```

## Dead Code

### Remove unused code

* You can find it in the version control system
* Check out warnings for this
* Leave the code clean from dirt

### Comments

Prone to
* being out-of-date
* copy-paste error

## Error Handling

### Two types of exceptions

* Expected or business exceptions ~ _checked?_
* Unexpected program or environment errors ~ _unchecked?_

### Good Practices

* Prefer exceptions to return codes - _decreases pollution of clients_
* Prefer exception types to exception payload - _error codes_
* Provide context for exception:
  * chain exceptions when wrapping
  * add erroneous object(s)
* Do not return null - _throw exception (e.g. IllegalArgumentException)_
* Prefer runtime exceptions to checked exceptions - _decreases pollution and dependency_
* Wrap exceptions in module or service specific exceptions - _decrease dependency_
* Only unexpected exceptions should be logged on error level with stack-trace.

### Bad Practices

* Swallow exceptions
* Implement business logic in catch block
* Do not catch exceptions unless you handle them
* `handleError()` type of methods - 
  * _not readable what they do_
  * _they cheat the compiler too_

## Classes

### Two Types of Classes

#### Procedural

Business logic or Service

* Stateless, singleton or static if possible
* Instantiated mostly by the DI framework - _Spring, Java EE_
* If stateful, create it from the code with `new`

#### Data structure

Entity, DTO (Data Transfer Object)

* Only data members
* No business logic
* Always instantiated as new - _by the database layer or with new from the code_
* Accessors/mutators are questionable - _getters/setters_

### Rules

* One reason to exist, change
* "Small"
* No "God" class - _"Sack", "Blob"_
* Encapsulation (hiding, protection) decreases dependency - _Other classes cannot depend on this_
* Tight cohesion

### Cohesion

* Implements the "one thing" rule
* Contains only dependent members
* Refactor to cohesive classes
* There will be many small classes - _Like a toolbox with drawers_
* Reduces amount, cost and risk of changes

### Interfaces

* Create interfaces for service classes -_but not always paranoidly for everything_
* Prefer interfaces to parent classes
* Create marker interfaces

### Smells

#### No meaningful name

* You cannot give a meaningful name - _e.g. "Parent", "Common", "Processor", etc._

#### Unnecessary polymorphism

* Polymorphic class is not used as polymorphic - _never declared to parent type - see later_

#### Does more things - Low cohesion

* Many methods - _"God" or "Blob" class_
* Methods of a class can be split into distinct call chains - _they should be in separate classes_
* Test coverage is not visible or cheating
* Refactor to composition + Facade pattern

Example: Refactoring low cohesion

![](https://petozoltan.github.io/images/clean-code-outline/refactoring-low-cohesion.png)

## Formatting

### Rules

* Increases readability and expressiveness
* Put close to each other what belongs together

### Vertical

* Member variable declarations at the top of the class
* Local variable declarations prior to their usage - _not at the top of the block_
* Use empty lines - _but only one_
* Write in order of execution and calls
* Write similar methods close to each other

### Horizontal

* Limit line length - _100-120 characters_
* The reader should not scroll to the right
* Use white space
* Use correct indentation
* Do not use tabular formatting

### Blocks

* Always put braces
* Always put braces for empty blocks too

### Good practices

* Agree on formatting in project
* Use your IDE's capabilities - _default is often good_
* Break long expressions into more lines
* Do not deviate too much from Java Code Conventions (Sun, 1997)

## Unit Tests

It is not part of this document, find only some thoughts here.

> Clean Code = Testable Code

### Rules

* Continuously write unit tests
* Maintain unit test - _keep them running_
* TDD - Test Driven Development
* Tests must be clean too - _they will change with the code_
* Tests must obey the test patterns
* F.I.R.S.T. principles

### Benefits

Enforces to write testable code
Makes the code flexible - _changes with regression tests_

### Code coverage

* Try to reach higher levels (>90%)
* Do not write tests only for the sake of the code coverage

### Good practices

* Use the default (package) visibility for the sake of the unit testing

Unit Testing briefly:

![](https://petozoltan.github.io/images/clean-code-outline/test-automation-overview.png)

## Warnings

* Do not ignore compiler/IDE warnings
* Each warning is a potential/existing bug
* Do not suppress warnings - _Find the correct solution instead_
* Use the capabilities of your IDE - _Turn on most of the possible warnings_
* Do not add new code with warnings!
* Use code checkers - _CheckStyle, FindBugs, PMD, Sonar, etc._

Example: Bad: Suppressed warnings

``` java
// Many tricks for one unused parameter

// CHECKSTYLE:OFF
@SuppressWarnings("unused")
private void addDescription(Type type, Contract contract, String comment) { // NOSONAR
    contract.setDescription(createDescription(contract.getType(), comment));
}
// CHECKSTYLE:ON
```

Example: Good: Fixed problems

``` java
private void addDescription(Contract contract, String comment) {
    contract.setDescription(createDescription(contract.getType(), comment));
}
```

## Logging

* Use correct logging levels
* Log stack trace only for unexpected program errors
* Create (concatenate) expensive message only if logged - _see SLF4J capabilities_

## Java

* Never use raw types - _always use generics correctly_
* Avoid using reflection
* Know you API - _use utility methods_

## Object Oriented Programming

### OOP Paradigm

The original paradigm just to remember:
* Encapsulation
* Inheritance
* Polymorphism

### Clean OOP Principles

* Tight cohesion
* Loose coupling
* Responsibility - _where to write code?_

### Separation of concerns

* Creation - _Dependency Injection_
* Configuration
* Services, components - _Business logic_
* Data - _Entities, DTOs_
* Layers
* Logging - _Framework or AOP_

### Dependency Injection

#### Dependency Inversion

* The paradigm
* A.k.a. Inversion of Control, IoC
* Always depend from the abstraction
* The more abstract, the more robust

Example: What is inverted in DI?

![](https://petozoltan.github.io/images/clean-code-outline/uml-dependency-inversion.png)

#### Dependency Injection

* Implementation of the Dependency Inversion
* Mostly done by a DI framework -Spring, Java EE, ...
* Easy to test -using mocks, test doubles

Example: Bad: Without dependency injection

``` java
public class FileHistoryService {

    // Factory - Hard to replace implementation, hard to test
    private IFileHistoryDao fileHistoryDao = DaoFactory.getFileHistory();

    // Instantiation - Depends on implementation, may be more complex
    private FileHistoryToFileHistoryDtoAssembler fileHistoryAssembler = new FileHistoryToFileHistoryDtoAssembler();

    // Static methods - Depends on implementation, not polymorphic
    private FileHistory createFileHistory() {
        HttpHistoryAuthorHelperTAFile.fillAuthorFromHttpRequest(fileHistory);
    }
}
```

Example: Good: Dependency injection by a DI framework

``` java
@Component
public class FileHistoryService {

    @Autowired
    private IFileHistoryDao fileHistoryDao;
    @Autowired
    private FileHistoryToFileHistoryDtoAssembler fileHistoryAssembler;
    @Autowired
    private HttpHistoryAuthorHelperTAFile authorHelper;
}
```

### Inheritance over instanceof

Do not use instanceof and isAssignableFrom()

* it adds dependency
* it adds duplication
* refactor to polymorphism or patterns

### Composition over inheritance

#### Problems with inheritance

* Too strict
* Hard to develop - _one child changes a certain way the other one does not_
* Do not use inheritance only for a "common" code
* Parent and children are be changed together - _spaghetti code_
* Favor composition to inheritance - _Item 16 in Effective Java (2nd Edition, Joshua Bloch, 2008)_
* Overridden methods are unreadable and fragile - _Item 17 in Effective Java (2nd Edition, Joshua Bloch, 2008)_

#### Code Smells

* Parent must be changed when children change, abstract methods should be added
* The parent's name is "Common..." - _a class should have an intentional business name_

#### Use inheritance only for

* Real polymorphism
* Polymorphic usage - _declared as a "parent" type_
* Design patterns

### Law of Demeter

* "Only talk to immediate friends"
* Do not depend on the implementation details other classes
* Use only one level of abstraction
* "Wallet" rule
* "Count of dots" rule - _But not simply a dot counting law_
* It depends on that the used class is procedural or a data structure (see Classes)

Example: Bad:

``` java
// Depends on implementation of neighbors of neighbors...
String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

// More levels of abstraction, reaches through layers
public boolean checkPassword(String name, String pwd) {
    userService.checkPassword(pwd); // It already uses UserDao
    User user = userDao.findUser(name); // It should not
}
```

### S.O.L.I.D.

Not in the book but also Uncle Bob.

#### Single Responsibility

* A class should have only one reason to change
* Only a change in the specification should affect the implementation of the class

#### Open/Closed

* Software entities should be open for extension, but closed for modification

It can be more general:
* Software entities should NOT be open for extension
* Any class should be closed for modification - _not only parent classes_

#### Liskov Substitution

* Objects should be replaceable with instances of their subtypes without altering the correctness of that program.
* See also design by contract

#### Interface Segregation

* Many client-specific interfaces are better than one general-purpose interface.

#### Dependency Inversion

* Depend on Abstractions. Do not depend on concretions.
* Dependency injection is one method of following this principle.

## Related Posts

* [Clean Code Smells TOC](https://petozoltan.github.io/2016/08/19/clean-code-toc.html#smells)
* [Clean Code TOC](https://petozoltan.github.io/2016/08/19/clean-code-toc.html)
* [Clean Code Links](https://petozoltan.github.io/2016/08/20/clean-code-links.html)
* [Effective Java TOC](https://petozoltan.github.io/2016/08/19/effective-java-toc.html)
