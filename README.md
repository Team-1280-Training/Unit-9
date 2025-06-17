# Unit 9: Additional Topics

## Introduction
You're one unit and a final project away from completing our beginner training! At this point, you know most of the Java basics you'll need going into the programming subteam, but there are some miscellaneous topics left to cover.

Unit 9 contains various unrelated topics and skills that aren't as fundamental but are still important or useful. There are no exercises and no project.

### Table of Contents
- [Research](#research)
    - [AI](#ai)
- [Enums](#enums)
- [Code Readability](#code-readability)
    - [Complexity](#complexity)
- [Lambda Expressions and Method References](#lambda-expressions-and-method-references)
- [Type Casting](#type-casting)
- [Recap](#recap)

[Feedback](#feedback) \
[License](#license)

## Research
Programming is a unique subject (compared to math, chemistry, etc.); knowledge is readily available and easily applicable. \
An important skill that you will be using constantly as a programmer is **self-learning**.

In this course, all of the necessary information has been provided in one location, the lesson. \
After this course, you will need to search for all of the information yourself, primarily on the web and in **documentation** (docs).

Say you come across something new, or you don't know how to implement a certain thing, or you forgot the methods of a class. \
The first step is to search it up on a browser, of course. (Include only the necessary words; a browser searches mostly by terms, not by grammar or phrasing. Usually you need to add the language name too.) \
Example search phrases:
```
java modulus operator
java arraylist get index of value
```
In Google Chrome, you can wrap a term or phrase in double quotes `""` to search for that exact spelling or phrase.

`stackoverflow.com` is a site where other programmers ask questions and get answers, so you can find many solutions to previously-asked, common problems there. \
For broader or general information, often for a library or class, documentation sites are provided by the creator. You may have to use `Ctrl`+`F` to find specific information. \
As an example, see https://docs.oracle.com/javase/8/docs/api/java/lang/String.html; this specific format and styling is common for documentation in the Java ecosystem. Methods are listed out with their name, return type, parameters, and description. 

Good places to research are code examples and existing codebases. \
Documentation often shows code snippets and libraries sometimes have example programs. \
Existing codebases, such as robot codebases from previous years, are the best for reference. (These codebases are almost always on GitHub.)

In VS Code, there are also ways to view information from the code. \
In a method call, hover over a method name to see information about it. You can also press `Ctrl`+`Space` to trigger suggestions: e.g. to show overloads or autocomplete. \
The autocomplete also is convenient for browsing all methods; put just `object.` and the dropdown shows all available methods for the object.

`Ctrl`+`LeftClick` on a symbol to jump to its definition (for variables, methods, classes, goes to its declaration). \
If you `Ctrl`+`LeftClick` on the symbol at its definition itself, it instead pulls up all *references* to the symbol.

Note that most code actions are also available by right-clicking the code, for the dropdown.

### AI
*Artificial intelligence* (AI), specifically *large language models* (LLM) such as *ChatGPT*, *Windsurf*, *Claude*, and *Gemini*, are changing many aspects of programming. \
There are two primary uses of AI in programming:
- Researching information or asking questions
- Writing code or debugging

The first use is usually not harmful; it makes certain information faster to access and can answer even niche questions (replacing `stackoverflow`). \
Also, if AI gets it wrong then it isn't too consequential, and is easy to check (compared to other subjects).

However, we strongly recommend avoiding the second use; AI-powered code autocomplete and prompted code generation reduces the programmer's skills. \
Additionally, it has a very high rate of errors and mistakes, so it often isn't very useful or worthwhile.

Some general information about these AIs that you should keep in mind:
- Responses are much better and more accurate for common topics widely available on the web; specific libraries and tools lead to more errors or less useful information.
- AI is very confident in its answers even when they are wrong or don't know much. Be cautious with the information it gives.
    - AI sometimes makes up nonexistent knowledge; these are called hallucinations. For example, it may use a method that does not exist.
- The quality of AI responses decreases exponentially as complexity rises. AI is best at broad overviews and simple questions that reach only into superficial knowledge.

## Enums
An **enum** (enumeration) is a special kind of class we use to represent a set of options, often only as an identification (no value associated). \
By default, these constants have modifiers `public`, `static`, and `final`.

We can create and use enums like this:
```java
public class Main {
    enum Time {
        MORNING,
        AFTERNOON,
        EVENING,
        NIGHT
    }

    public static void main(String[] args) {
        Time currentTime = Time.MORNING;
        System.out.println("It is " + currentTime);
        // Output: It is MORNING
    }
}
```
Here, we declared an enum *inside* a class, but they can also be declared separately. \
The enum is the type, the constants are considered instances.

The main use of enums is for storing and checking an 'option', with if statements or switch statements.

Example:
```java
public class Main {
    enum CelestialBody {
        STAR,
        PLANET,
        MOON,
        ASTEROID
    }

    public static void main(String[] args) {
        CelestialBody object = CelestialBody.MOON;
        switch (object) {
            case STAR:
                System.out.println("Wow, a star! So bright!");
                break;
            case PLANET:
                System.out.println("Ooh, a planet! Is it habitable?");
                break;
            case MOON:
                System.out.println("Cool, a moon! Ours is better though.");
                break;
            case ASTEROID:
                System.out.println("AAAAAH, AN ASTEROID!!");
                break;
        }
        if (object != CelestialBody.STAR) {
            System.out.println("What's it made of?");
        }
    }
}
```
Output:
```
Cool, a moon! Ours is better though.
What's it made of?
```

The enum also has a static method `values()` that returns an array of the enum constants, in order. This is often used with for each loops.
```java
public class Main {
    enum CelestialBody {
        STAR,
        PLANET,
        MOON,
        ASTEROID
    }

    public static void main(String[] args) {
        System.out.println("What can we see in space?");
        System.out.println("We can see a lot! Here are a few common celestial bodies:");
        for (CelestialBody object : CelestialBody.values()) {
            System.out.println(object);
        }
    }
}
```
Output:
```
What can we see in space?
We can see a lot! Here are a few common celestial bodies: 
STAR
PLANET
MOON
ASTEROID
```

They have many other features too, which you can research if you need them.

## Code Readability
**Readability** is how easy it is to understand code. This is especially important when working with others, but it also benefits yourself as well. \
An unreadable codebase is much harder to maintain, debug, and extend. \
There are multiple things that contribute to readability.

Code formatting or styling is about the tiny details in how the code is written (they don't affect the code's behavior). \
Examples include whitespace, indentation, and how long lines are (line length limit). \
Programmers typically use a **formatter** to automatically format code. This standardizes how code is styled, which is especially important for shared codebases. \
In VS Code settings, turn on `Format On Save` setting to have the formatter run on save. To open *Settings*, press `Ctrl`+`,`. \
We recommend you use a formatter. It saves effort, and it also handles indentation for you. \
About optional blank lines: place them as needed to group code, but do not overuse them.

A critical part of code readability is proper naming of variables, methods, etc. \
First, the correct style should be used (variables, fields, and methods: `camelCase`, constants: `UPPER_CASE`, classes: `PascalCase`). \
Second, a descriptive name should be given. In some cases, this can be difficult. \
Make sure variable names are concise yet informative. Avoid including the type (e.g. `int`, `String`, array) in the name. Be consistent with terminology and other names in the program. \
Also, collections are typically the element name but pluralized (e.g. `Player player;` -> `ArrayList<Player> players;`).

A program is simpler and more understandable when it is **consistent**. \
This includes having a coherent terminology, using conventions, and structuring code in similar ways. \
Use previously written code in the codebase as examples, to improve consistency. (Or, **refactor** (rewrite) code as needed.)

**Documentation**, in general, refers to any descriptions or information about code. External docs (e.g. websites) are one source, but information is embedded in code as well. \
Use comments to provide additional information that isn't already apparent from the code itself. \
Often, they focus on the *why* (intention, purpose) rather than the *how* (what the code does). \
Methods may have standard Javadoc comments, which are multi-line comments placed before a method declaration that start with `/**` instead of `/*`.

### Complexity
Minimizing complexity is crucial for readability. \
This is done with abstraction and simplifying code structure.

One principle of abstraction is that methods should be singular, discrete actions. Even if the method is only used once, it helps make methods smaller and documents what it does. \
A class should have focused responsibility and functionality.

In general the more nested (indented) code is, the more complex it is. Simple tactics can reduce nesting. \
Extract code out into methods, reducing indentation. \
Use early `return` or `continue` (guard clauses), and invert conditionals to reduce nesting.

The ternary operator is a shorter way of if-else statements for deciding between two values based on a condition.
```
condition ? expressionIfTrue : expressionIfFalse
```
(Values, variables, etc. count as expressions.)

For conditional statements and loops, if the body contains only one statement then the braces can be omitted. Many discourage this practice, but you may see it sometimes, especially for guard clauses.

<details><summary>Example complexity reduction</summary>

Original:
```java
/**
 * Gives an ArrayList of booleans for whether each number is even
 * 
 * Returns null if the input is null.
 * Elements in the returned list are null if the input element is null.
 * 
 * @param numbers null, or ArrayList of null or Integer
 * @return null, or ArrayList of null or Boolean
 */
ArrayList<Boolean> elementsEven(ArrayList<Integer> numbers) {
    ArrayList<Boolean> result = new ArrayList<>();
    if (numbers != null) {
        for (Integer number : numbers) {
            if (number != null) {
                if (number % 2 == 0) {
                    result.add(true);
                } else {
                    result.add(false);
                }
            } else {
                result.add(null);
            }
        }
        return result;
    } else {
        return null;
    }
}
```
Simplified:
```java
ArrayList<Boolean> elementsEven(ArrayList<Integer> numbers) {
    if (numbers == null) return null;
    ArrayList<Boolean> result = new ArrayList<>();
    for (Integer number : numbers) {
        Boolean element = (number == null) ? null : (number % 2 == 0);
        result.add(element);
    }
    return result;
}
```
</details>
Additionally, for most code, try to make each statement perform only one action. (For example, extract calculation results into variables before using them.)

## Lambda Expressions and Method References
Lambda expressions are used to define unnamed ('anonymous') methods/functions. \
The syntax is as follows (any number of parameters of course):
```java
(param1, param2) -> returnExpression
```
Or:
```
(param1, param2) -> {
    statement;
    statement;
}
```
When called, the first runs and returns just that expression, while the second executes an actual body of statements (which may include a `return` statement). \
The parameters do not need their types declared.

Examples:
```
(x, y) -> x + y
(x, y) -> {
    System.out.println(x + y);
    return x + y;
}
```

These lambdas are objects and are usually passed into methods. \
Example:
```java
new InstantCommand(() -> setSafety(false))
```
Another related construct is method references, which allow you to pass around methods as objects. These have the same uses as lambda expressions.

Syntax:
```
object::method
```
(So, replace `.` with `::` in method access.) \
Example:
```java
drivetrain.registerTelemetry(logger::telemeterize);
```
The declared type for lambda expressions and method references are *functional interfaces*. These will not be taught. They are usually defined for you already, if for some reason you need to use them.

Lambda expressions and method references are advanced features of Java and you won't need to use them in this course. \
They are prominent in certain libraries, however.

## Type Casting
**Type casting** is the process of converting a value from one type to another, usually primitives.

There are two kinds of type casting, *widening casting* (upcasting) and *narrowing casting* (downcasting).

To cast a value into another type, use the casting operator:
```
(DataType) value
```
```java
int x = (int) 2.0;
```
The operator precedence is higher than arithmetic operators.

**Widening casting** is done *automatically* (implicitly), and converts a value from a smaller data type to a larger data type. It can be done manually if needed. \
Widening casting is when the target data type is larger than the source type.

It happens implicitly in variable assignments. \
Sometimes done manually, such as to avoid integer division truncation.

We can do this with these data types in the following order (also related to precision):
`byte` -> `short` -> `int` -> `long` -> `float` -> `double`

Example:
```java
double x = 5; // x is 5.0
double y = (double) 2 / 4; // y is 0.5 = 2.0 / 4
```
Here, the `int` value `5` is automatically converted to a `double`, and `2` is manually converted to a `double` so that the division results in a `double`.

**Narrowing casting** must be done *manually* (explicitly), and converts a value from a larger data type to a smaller data type.

Example:
```java
int x = (int) 2.5; // x is 2
```
In this example, we have to use narrowing casting or we'll get an error. \
Note that we *do* lose data when we cast `2.5` as an `int`. The value is *truncated*, meaning the digits after the decimal point are removed, not rounded.

For non-primitive (object) types, casting *does not actually change the object's value* at all, but just changes the declared type of the object. Polymorphism is related to implicit widening casting. \
You can declare that a less specific superclass object is actually of a subclass type with narrowing casting; if it is not actually the case, then an exception is raised.

## Recap
- Self-learn topics on the web, in documentation, and from code examples and existing codebases
- AI is fine for simple questions and quick research, but avoid generating code with it
- An `enum` is a set of constants that are used to define multiple different options; use them with `if` and `switch` statements
- To improve readability: use a formatter, name variables well, be consistent, document your code, and reduce code complexity
- To reduce code complexity: use abstraction, break up your code into organized pieces, and reduce nesting/indentation via extraction and guard clauses
- The ternary operator gives one of two values based on a condition; syntax is `condition ? expression1 : expression2`
- Braces may be omitted for single-liner conditional statements and loops; this is usually discouraged
- Lambda expressions define anonymous functions, with, e.g.: `(x, y) -> x + y` and `(x, y) -> { System.out.println(x + y); return x + y; }`
- Type casting happens implicitly for widening, but may be done manually for either direction with `(DataType) value` casting operator
- Narrowing casting usually loses data for primitives, while, for objects, casting does not change them but may raise an error when the actual type doesn't match

### Keyboard Shortcuts
| Keybinding | Command |
| - | - |
| `Ctrl`+`Space` | Trigger suggestions |
| `Ctrl`+`LeftClick` | Jump to definition of symbol |
| `Ctrl`+`,` | Open *Settings* tab |

## Feedback
Please provide feedback if you have any.
<details><summary>Possible feedback points</summary>

- Confusing explanations
- Knowledge, skills, or procedures that were required but weren't taught
- Too fast or too slow explanations; pacing
- Too hard or too easy exercises
- Step-by-step instructions that are not comprehensive/thorough enough, or didn't work
- Seemingly unnecessary or ineffective information or exercises
- Any improvements (e.g. wording) or more effective ways/formats to teach
</details>

___



## License
© 2025 @aatle, @spacepotatoes3, @gjgarson, @KaitoTLex

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
