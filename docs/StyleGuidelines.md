Neurala's Style Guide
=============

Neurala's General Style Guidelines for C-based Languages

<a name="toc"></a>Table of Contents
-----------------------------------

* [General](#general)
    * [Naming](#naming)
    * [Pointer Asterisks](#pointerAsterisks)
    * [Whitespace](#whitespace)
    * [Braces](#braces)
    * [Line Breaks](#linebreaks)
    * [Indentation](#indentation)
    * [Literals](#literals)
    * [File Structure](#filenames)
    * [Commenting](#commenting)
* [C++](#cpp)
     * [Indentation](#cppindentation)
     * [Naming](#cppnaming)
     * [Casting](#cppcasting)
     * [auto Keyword](#cppauto)
     * [For and For Each](#cppfor)
     * [Pointers](#cpppointers)
     * [Inheritance](#cppinheritance)
	 * [Using Libraries](#cpplibraries)
* [Objective-C](#objC)
     * [Method Naming](#objCMethods)
     * [Organization](#objCorganization)
     * [Enumerated Types](#objCEnumerated)
     * [Dot Notation Syntax](#objCdotnotation)
     * [Constants and enum Prefixes](#objCprefixes)
     * [File Names and Extensions](#objCfiles)
     * [NSLogs](#objCNSLogs)
     * [@synthesize](#objCsynthesize)
     * [self.variable vs. _variable](#objCselfdot)
     * [Blocks](#objCblocks)
     * [Documentation Commenting](#objCdocumentation)

* [Influences](#influences)


<a name="General"></a>General
-------------------------------


### <a name="naming"></a>Naming

* Variable names should be [camelCase](http://c2.com/cgi/wiki/wiki?CamelCase)
~~~~~~~~~~~~~~~{.cpp}
int foobar; // Wrong
int foo_bar; // Also wrong

int fooBar; // Right
~~~~~~~~~~~~~~~

* Class names should be [WikiCase](http://c2.com/cgi/wiki/wiki?WikiCase):
  * Similar to [camelCase](http://c2.com/cgi/wiki/wiki?CamelCase), but starts with capital letter
~~~~~~~~~~~~~~~{.cpp}
class foobar; // Wrong
class fooBar; // Wrong
class Foobar; // Wrong
class Foo_Bar; // Wrong

class FooBar; // Right
~~~~~~~~~~~~~~~


* Names for variables should be clear, descriptive, and nonambiguous. 

```objc
int currentBehaviorIndex; // Right

int curBehX; // Wrong
```

* Avoid "magic numbers" with no meaning attached. 

```objc
if (pin.length < pinSizeMax)  // Right

if (pin.length < 5) // Wrong

```

#### <a name="pointerAsterisks"></a>Pointer Asterisks

* Pointer Asterisks should be attached to the type, not the variable name.


```objc
type* variableName; // Right

type *variableName; // Wrong

```

#### <a name="whitespace"></a>Whitespace

* With if statements, parentheses should hug the condition, but a
space should exist between the if and the parentheses.
~~~~~~~~~~~~~~~{.cpp}
if( condition ) // Wrong

if (condition) // Right
~~~~~~~~~~~~~~~

* Operators should be surrounded with spaces except for the ++ operator and the ! operator.
~~~~~~~~~~~~~~~{.cpp}
if (foo==bar) // Wrong
foo=bar+1 // Wrong

if (foo == bar) // Right
foo = bar + 1; // Right
~~~~~~~~~~~~~~~



#### <a name="braces"></a>Braces

* Braces should be on their own lines and be inline with the parent.
* Single line if statements should be surrounded by braces
~~~~~~~~~~~~~~~{.cpp}
// Wrong
if (foo == bar)
	doSomething();

// Wrong
if (foo == bar) doSomething();

// Wrong
class Foo {
	... // some code
	}

// Wrong
class Foo
	{
		... // some code
	}

// Wrong
if (condition) {
	... // some code
} else {
	... // more code
}

// Right
if (foo == bar)
{
	doSomething();
}

// Right
class Foo
{
	... // some code
}

// Right
if (condition)
{
	... // some code
}
else if (condition)
{
        ... // some code
}
else
{
	... // more code
}
~~~~~~~~~~~~~~~

* Case statements should indent another level
~~~~~~~~~~~~~~~{.cpp}
switch(foo)
{
// Wrong
case bar:
	... // some code

// Right
	case bar:
		... // some code
}
~~~~~~~~~~~~~~~


#### <a name="linebreaks"></a>Line Breaks

* Try to keep lines below 100 characters long.

* Indent long lines before operators
~~~~~~~~~~~~~~~{.cpp}
int foo = doSomeOperationWithAReallyLongName(someReallyLongVariable)
          + someOtherReallyLongVariableName
          + whyAreTheseVariableNamesSoLong;
~~~~~~~~~~~~~~~


#### <a name="indentation"></a>Indentation

* Use tabs for indentation and spaces for alignment
~~~~~~~~~~~~~~~{.cpp}
int someFooBar = 0;
for (int index = 0; index < 10; ++index)
{
	// This line is indented with a tab
	someFooBar += someLongMethodName(index)
	// This line is indented with a tab and aligned with spaces
	           + someOtherLongMethodName(index)
}
~~~~~~~~~~~~~~~


* When a function takes a long string of arguments and exceeds 100 characters, default to aligning the variables on new lines.

```
x = foo(a,
        b,
        c,
        d);
```

* In certain instances, it may drastically increase readability to group the functions logically.
```
x = foo(x1, y1
        x2, y2
        x3, y3
        x4, y4);
```

* When a nested indentation involves another nested indentation, handle it like this:

```
x = foo(a,
        b,
        bar(c, 
            d));
```

#### <a name="literals"></a>Literals

Literals should be uniform across the codebase. 

```objc
float floatingPoint = 1.0f; // Right
double doubleExample = 1.0; // Right

float floatingPoint = 1.f; // Wrong
float floatingPoint = .1; // Wrong
float floatingPoint = 1; // Wrong
double doubleExample = 1.; // Wrong
double doubleExample = 1; // Wrong
```

#### <a name="filenames"></a>File Structure
* File names should be exactly the same as the name of the class implementation they contain- including the case.
* Multiple classes should not be implemented in the same file.


#### <a name="commenting"></a>Commenting

##### Commenting Spacing

* Comments should have a space between the forward slash and the body of the comment.

```objc
// This is a comment on today's sociopolitical state.  // Right


//This is a bad comment on today's sociopolitical state. // Wrong
```

##### When to comment

* If code requires a lot of comments to explain what it is doing, it is frequently a sign of deeper issues(see: [code smell](http://en.wikipedia.org/wiki/Code_smell "Code Smell")). Try to write clear code that is self-documenting and requires minimal commenting. Then, when necessary, add in short comments that explain **why** something is being done a particular way rather than how it does it. 

##### NOTE, TODO, OPTIMIZE, HACK, XXX, BUG

These identifiers can be left to make a comment more specific and easily searchable:
* `NOTE:` Description of how the code works (comments are used for *why*)
* `TODO:` No inherent problem, but additional code needs to be written such as a new feature before something can be used or written.
* `OPTIMIZE:` code achieves expected results but has serious potential to be faster or more efficient
* `HACK:` code achieves expected results but does so in ways that break the style guidelines or design patterns or is just plain hacky. 
* `XXX:` or `WARNING:` Used as a warning for a workaround in 3rd party code or as caution to someone looking at or modifying the code as to why something is done in a particular way that may seem inelegant or messy at first glance.
* `REFACTOR:` Something is wrong with this section of code but refactoring is required to fix it. 
* `BUG:` There is a problem here








<a name="cpp"></a>C++ Style Guidelines
-------------------------------

#### <a name="cppindentation"></a>Indentation

* Namespaces should not increase indentation level
~~~~~~~~~~~~~~~{.cpp}
namespace foo
{

	class Bar(); // Wrong

class Bar(); // Right

}
~~~~~~~~~~~~~~~

* Functions should have the type on a separate line in the implementation.
~~~~~~~~~~~~~~~{.cpp}
// Wrong
int Foo::barBaz()
{
	... // do something
}

// Right
int
Foo::barBaz()
{
	... // do something
}
~~~~~~~~~~~~~~~

* Initialization list should be indented along with colon using spaces.
~~~~~~~~~~~~~~~{.cpp}
// Wrong
Foo::Foo(int foo) : m_foo(foo)
{
	... // do something
}

// Wrong
Foo::Foo(int foo) :
         m_foo(foo)
{
	... // do something
}

// Right
Foo::Foo(int foo)
   : m_foo(foo)
{
	... // do something
}
~~~~~~~~~~~~~~~

#### <a name="cppnaming"></a>Naming
* Class private member variables should be prefixed with 'm_'.
~~~~~~~~~~~~~~~{.cpp}
// Wrong
class Foo
{
	Bar bar;
 ... // more code
};

// Right
class Foo
{
	Bar m_bar;
 ... // more code
};
~~~~~~~~~~~~~~~

* Getters and setters should just be the member name without the 'm_'.
~~~~~~~~~~~~~~~{.cpp}
// Wrong
class Foo
{
	Bar m_bar
 ... // more code

public:
	Bar getBar() { return m_bar; }
	void setBar(Bar bar) { m_bar = bar; }
};

// Right
class Foo
{
	Bar m_bar;
 ... // more code

public:
	Bar bar() { return m_bar; }
	void bar(Bar bar) { m_bar = bar; }
};
~~~~~~~~~~~~~~~

#### <a name="cppcasting"></a>Casting


* Prefer static_cast, const_cast, reinterpret_cast to C style casts

#### <a name="cppoperators"></a>Operators

* Prefer prepending over appending ++.

~~~~~~~~~~~~~~~{.cpp}
// Wrong
i++;

// Wrong
for (int i = 0; i < 10; i++)
{
	... // some code
}

// Right
++i;

// Right
for (int i = 0; i < 10; ++i)
{
	... // some code
}
~~~~~~~~~~~~~~~

#### <a name="cppauto"></a>auto Keyword

'auto' keyword can be used in the following cases. If the auto could
make the code less readable, do not use it.

* When it avoids repetition of a type in the same statement.
~~~~~~~~~~~~~~~{.cpp}
auto foo = new Foo;
auto foo = static_cast<Foo *>(bar);
~~~~~~~~~~~~~~~

* When assigning iterators.
~~~~~~~~~~~~~~~{.cpp}
auto it = someVector.const_iterator();
~~~~~~~~~~~~~~~

####  <a name="cppfor"></a>For and For Each

* Optionally use for each loops for readability:
~~~~~~~~~~~~~~~{.cpp}
for (auto&& elem : someVector)
{
	... // some code
}
~~~~~~~~~~~~~~~

#### <a name="cpppointers"></a>Pointers


Prefer C++11 smart pointers to normal pointers, especially for
member variables. The default pointer type should be std::unique_ptr

#### <a name="cppinheritance"></a>Inheritance

* Prefer composition over inheritance.
* Avoid multiple inheritance except from pure abstract classes.

* When subclassing and overriding a virtual function, use the "override" keyword:
* Use the "final" keyword to mark when a virtual function or a struct should not be overriden.

~~~~~~~~~~~~~~~{.cpp}
class Foo
{
public:
	virtual void bar();
};

class DelightfulFoo : Foo
{
public:
	virtual void bar(); // Wrong
	virtual void bar() override; // Right
};
~~~~~~~~~~~~~~~

### <a name="cpplibraries"></a>Using Libraries

* When writing a library always enclose the API in namespaces.
* Don't use the "using" keyword to import namespaces. Instead, explicitly write out the namespace.





<a name="objC"></a>Objective-C Guidelines
-------------------------------

#### <a name="objCMethods"></a>Method Naming

* In method signatures, there should be a space after the method type (-/+ symbol). Additionally, there should be a space between the method segments (matching Apple's style).  Always include a keyword and be descriptive with the word before the argument which describes the argument.

* The usage of the word "and" is reserved.  It should not be used for multiple parameters as illustrated in the `initWithWidth:height:` example below. It is instead reserved for described two separate actions, like in the `openFile:withApplication:andDeactivate:` example. In many of these instances, it is often better to split the function into two separate functions. 
* Method names that are significantly longer than 100 characters should be broken up over multiple lines using colon alignment. 

**Preferred:**
```objc
- (void)setExampleText:(NSString*)text image:(UIImage*)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
- (BOOL)openFile:(NSString*)fullPath withApplication:(NSString*)appName andDeactivate:(BOOL)flag;
```

**Not Preferred:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  
- (BOOL)openFile:(NSString*)fullPath withApplication:(NSString*)appName Deactivate:(BOOL)flag;
```

#### <a name="objCorganization"></a>Organization

* Put `init`, `dealloc`, and their associated helpers and functions at the top of an implementation.  
* Group functions with similar puprposes and use `#pragma mark -` to categorize groups of methods.
* Keep all delegate functions together and in the same order with a `#pragma mark -` denoting what delegate they are.


#### <a name="objCEnumerated"></a>Enumerated Types

* When using `enum`s, use the new fixed underlying type specification. This provides stronger type checking and code completion. The SDK includes a macro to facilitate and encourage use of fixed underlying types: `NS_ENUM()`.


```objc
typedef NS_ENUM(NSInteger, EPokemonCards) {
    ePokemonCardBulbasaur,
    ePokemonCardIvysaur,
    ePokemonCardVenesaur
};
```

#### <a name="objCdotnotation"></a>Dot Notation Syntax
* Dot Notation Syntax Should be **always** used for accessing and mutating properties. Bracket Notation is preferred in all other instances. 

```objc
view.backgroundColor = [UIColor orangeColor]; // Right
[UIApplication sharedApplication].delegate; // Right

[view setBackgroundColor:[UIColor orangeColor]]; // Wrong
UIApplication.sharedApplication.delegate; // Wrong
```

#### <a name="objCprefixes"></a>Constant and enum Prefixes

* Constants should begin with a lowercase k, booleans should begin with a lowercase b or an `is` or a `should`. The name of enumerated types should have an uppercase E and all enumerators should have a lowercase e. 

```objc
ERewardFilters reward =  eRewardFilterTacticalVision; // Right
BOOL bConnected = YES; // Right
BOOL isConnected = YES; // Right
NSString* const kObjectCenterXKey = @"ObjectCenterXKey"; // Right


RewardFilters reward =  RewardFilterTacticalVision; // Wrong
BOOL connected = YES; // Wrong
BOOL kConnected = YES; // Wrong
NSString* const ObjectCenterXKey = @"ObjectCenterXKey"; //Wrong
```

#### <a name="objCfiles"></a>File Extensions 
* File extensions should accurately reflect the type of code within them. Specifically in our case, a file should **not** be Objective-C++ if it only contains objective c code. 

#### <a name="objCNSLogs"></a>NSLogs
* NSLogs should only be used to report errors. Remove NSLogs meant for personal debugging before pushing to remote branches. 


#### <a name="objCsynthesize"></a> @synthesize

* As of the middle of 2013, LLVM defaults to synthesizing accessors for properties. Because of this, using `@synthesize` is now unnecessary and discouraged. 


#### <a name="objCselfdot"></a> self.variable vs. _variable 
* In most instances, `self.variable` should be used instead of `_variable`. This helps with key value observing and computed properties. Be mindful of anytime you use `_variable`, as this should only be used when you intend to be access the value via reference.

#### <a name="objCblocks"></a>Blocks

* Objective-C Code blocks are inherently messy and have become the exception to most rules in style guidelines. We treat blocks as a special case and thuse they break two of our standard rules:
     * Do not colon align blocks.
     * Do not put brackets for blocks on their own lines. 
* Implement blocks as closely to Apple's code examples as possible, as this is one of the only ways to make blocks readable.

**Preferred:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
    // something
} completion:^(BOOL finished) {
    // something
}];
```

**Not Preferred:**

```objc
// colon-aligning makes the block indentation wacky and hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

or

```objc
// blocks are easily readable
// but the brackets look more confusing
[UIView animateWithDuration:1.0 animations:
^{
    // something
} 
completion:^(BOOL finished) 
{
    // something
}];
```


#### <a name="objCdocumentation"></a>Documentation Commenting

* All frameworks generate an appledoc file based off of the commenting in their public headers files. These comments are expected to be maintained and updated by the owner of the framework and they should conform to the Appledocs style. There is a full guide to this in our documentation folder.



<a name="influences"></a>Influences
-------------------------------
* [NY Times Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)
* [raywenderlich.com Objective-C Style Guide](https://github.com/raywenderlich/objective-c-style-guide)
* [Robots And Pencils Style Guide](https://github.com/RobotsAndPencils/objective-c-style-guide)
* [Google Objective-C Style Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
