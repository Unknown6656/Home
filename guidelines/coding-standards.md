Coding Guidelines for C#
===========================================

## Design & Maintainability

#### Basic Principles
* The Principle of Least Surprise
* Keep It Simple Stupid
* You Ain’t Gonne Need It
* Don’t Repeat Yourself

### Class Design
* A class or interface should have a single purpose
* An interface should be small and focused 
* Use an interface to decouple classes from each other
* Don’t hide inherited members with the new keyword
* It should be possible to treat a derived object as if it were a base class object 
* Don't refer to derived classes from the base class
* Avoid exposing the objects an object depends on
* Avoid bidirectional dependencies 
* Classes should have state and behavior

### Member Design
* Allow properties to be set in any order
* Don't use mutual exclusive properties 
* A method or property should do only one thing 
* Don’t expose stateful objects through static members
* Return an IEnumerable<T> or ICollection<T> instead of a concrete collection class 
* Properties, methods and arguments representing strings or collections should never be null 
* Define parameters as specific as possible

### Miscellaneous Design
* Throw exceptions rather than returning status values
* Provide a rich and meaningful exception message text
* Don't swallow errors by catching generic exceptions
* Always check an event handler delegate for null
* Properly handle exceptions in asynchronous code
* Use a protected virtual method to raise each event
* Don’t pass null as the sender parameter when raising an event
* Use generic constraints if applicable
* Evaluate the result of a LINQ expression before returning it

### Maintainability
* Methods should not exceed 7 statements
* Make all members private and types internal by default
* Avoid conditions with double negatives
* Don’t use "magic numbers" 
* Only use var when the type is very obvious
* Declare and initialize variables as late as possible
* Favor Object and Collection Initializers over separate statements
* Don’t make explicit comparisons to true or false
* Don’t change a loop variable inside a for or foreach loop
* Avoid nested loops
* Always add a block after keywords such if, else, while, for, foreach and case
* Always add a default block after the last case in a switch statement
* Finish every if-else-if statement with an else-part
* Be reluctant with multiple return statements
* Don’t use if-else statements instead of a simple (conditional) assignment
* Encapsulate complex expressions in a method or property
* Call the most overloaded method from other overloads
* Only use optional arguments to replace overloads
* Avoid using named arguments
* Don’t allow methods and constructors with more than three parameters
* Don’t use ref or out parameters
* Avoid methods that take a bool flag
* Always check the result of an as operation
* Don’t comment-out code

### Framework Guidelines
* Use C# type aliases instead of the types from the System namespace
* Build with the highest warning level
* Use Lambda expressions instead of delegates
* Only use the dynamic keyword when talking to a dynamic object
* Favor async/await over the Task

## Naming & Layout

####Pascal Casing
* Class, Struct *AppDomain*
* Interface *IBusinessService*
* Enumeration type *ErrorLevel*
* Enumeratiion values *FatalError*
* Event *Click*
* Protected field *MainPanel*
* Const field *MaximumItems*
* Read-only static field *RedValue*
* Method *ToString* (with the exception of unit tests which can be underscore seperated if required for readability)
* Namespace *System.Drawing*
* Property *BackColor*
* Type Parameter *TEntity*

#### Camel Casing
* Private field *listItem*
* Variable *listOfValues*
* Const variable *maximumItems*
* Parameter *typeName*

### Naming
* Use US English
* Don’t include numbers in variables, parameters and type members
* Don’t prefix fields
* Don’t use abbreviations
* Name an member, parameter or varialbe according its meaning and not its type
* Name types using nouns, noun phrases or adjective phrases
* Don’t repeat the name of a class or enumeration in its members
* Avoid short names or names that can be mistaken with other names
* Name methods using verb-object pair
* Name namespaces using names, layers, verbs and features
* Use an underscore for irrelevant lambda parameters

### Documentation
* Document all public, protected and internal types and members
* Avoid inline comments
* Only write comments to explain complex algorithms or decisions
* Don’t use comments for tracking work to be done later

### Layout
* Maximum line length is 130 characters.
* Indent 4 spaces, don’t use Tabs
* Keep one whitespace between keywords like if and the expression, but don’t add whitespaces after ( and before ).
* Add a whitespace around operators, like +, -, ==, etc.
* Always add parentheses after keywords if, else, do, while, for and foreach
* Always put opening and closing parentheses on a new line.
* Don’t indent object Initializers and initialize each property on a new line.
* Don’t indent lambda statements
* Put the entire LINQ statement on one line, or start each keyword at the same indentation.
* Add braces around comparison conditions, but don’t add braces around a singular condition. 

#### Empty lines
* Between members
* After the closing parentheses
* Between multi-line statements
* Between unrelated code blocks
* Around the #region keyword
* Between the using statements of different companies

#### Member order
1. Private fields and constants
2. Public constants
3. Public read-only static fields
4. Factory Methods
5. Constructors and the Finalizer
6. Events
7. Public Properties
8. Other methods and private properties in calling order
