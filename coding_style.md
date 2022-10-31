# Coding Style

**Avoid Whitespace Wars**

**Use .editorconfig**

**Line Length**

**Columns**

**Use reasonable, meaningful names**

**Document Interfaces and classes**

**Write meaningful comments for the next person.**

## Whitespace wars
Do not engage in whitespace wars.  You will find developers are insanely passionate about tabs vs. spaces, brace placement, splitting lines, `using` statements, `this.` usage, variable and function names, and tons more.

Avoid the war by following the coding style of the current file, current project, current team or company, whichever is closest to where you are working.

## Use .editorconfig
When possible lobby to use .editorconfig in your projects.  It is committed to source control, major editors all support it and it should be the arbiter in any style discussions.  Have a change process for updating your style.

## Humans are lousy at horizontal scrolling
Yes the compiler ignores whitespace and yes can write a 500-character line.  But good luck having anyone review the last 400 characters.  Humans in general are lazy.  Developers are lazier and will not scroll left to review a long line of code.  They all assume someone else did and no one sees the errors in the PR.  This is a form of "testing in production" but not one I support.  😀

Shortening lines:
* Break lines at punctuation and operators
* avoid multiple function calls on a single line (it makes the stack trace crazy ambiguous)
* avoid multiple statements on a single line.
* break the ternary into 3 lines with the condition and true/false values separate lines.

Comments worth writing should be worthy of a line of their own.

## Tabs vs. spaces
Consistency is the key here.  My preference is spaces because a space is a space no matter the place.  HTML scrunches whitespace into a single blank but hardly anything else does.

Mixing tabs and spaces makes code hard to review.  This is only exacerbated when devolopers have different size for tabs.  (My preference is 2 because I don't like the horizontal scrolling.)

## Columns (Ionic or Doric)
Humans are really good at scanning columnar data and code.  Trimming whitespace at line ending is good but not allowing multiple consecutive blanks is a horrid editor rule IMO.  I like to align enum values.

Which of these enum values is duplicated?  Which one is easier to see te error?

```
enum roygbiv {
    red = 1,
    orange = 2,
    yellow = 3,
    green = 4,
    blue = 3,
    indigo = 5,
    violet = 6,
}
```
```
enum roygbiv {
    red    = 1,
    orange = 2,
    yellow = 3,
    green  = 4,
    blue   = 3,
    indigo = 5,
    violet = 6,
}
```

If you are forced to eliminate consecutive spaces you can still get columns with some ugly-ish code in something like this.  Dunder Mifflin's chief would still argue with you though.  I've had to use one or more of these ugly constructs to avoid adding a formatting suppression rule exception.

```
enum roygbiv {
    red    /**/ = 1,
    orange /**/ = 2,
    yellow /**/ = 3,
    green /* */ = 4,
    blue  /* */ = 3,
    indigo /**/ = 5,
    violet /**/ = 6,
}
```

## Use reasonable, meaningful names
You can name a variable `x`, `index`, or `theIndexIntoTheArrayOfElementsToEnumerate`.  I can understand the first two.  I can understand the last one too.  But ... why would write a sentence to describe an integer?  Or a function name?  Or anything?

My rule of thumb is variable names are `nouns` method names are `verbNoun()`.  Occasionally a method name might have a condition `verbNounCondition()` when it's a handler.

Short, meaningful names is the goal.

## Document Interfaces and Classes
Repeating the name of the interface or class is not documentation.  Do not even bother writing it down.

Remember that code models real world stuff most of the time.  Describe the real world concepts, not code choices.

**Interfaces** describe a contract or idea.  Capture that.  Interface properties and methods describe the contract.  I think they are all worth 1-3 full sentences, grammatically correct and spell-checked.  More is code smell of something probably too complicated.  Less just opens up questions for those who come behind.  Remember you are writing comments for yourself 6 months from now, your team when you are on vacation, code reviewers, and whoever joins your team after you leave.

**Classes** often are the single implementation of an interface and can `<inheritdoc />` from the interface.  The class itself deserves enough information to justify why it exists, even it just mentions it is the only expected implementation of the interface.

Class that use composition of multiple objects are worth describing why composition is being used.  Describe everything in terms of the business, not other interfaces, classes or objects.

[Back](./projects_and_solutions.md)  [Next](./hiding_things.md)