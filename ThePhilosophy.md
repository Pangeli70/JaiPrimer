
The Philosophy of Jai
=====================

**THE JOY OF PROGRAMMING**

At some point after programming for many years, the line between “exciting programming adventure” and “please not another code refactoring” can start to disappear. Having to update the function declaration in the header when you change its signature gets old fast. When C was originally written in 1973, there was a good reason for all that header stuff, but today there isn’t.

Quality of life improvements afforded by the language can have quantifiable benefits to the productivity of the programmer using the language. (If you aren’t convinced of that, try programming anything in [Brainfuck](http://en.wikipedia.org/wiki/Brainfuck).) Compiling should be fast if not instantaneous, refactoring code should require a minimum of changes, and error messages should be helpful and pleasant. The belief is that an improvement of the tools that programmers use can produce more than a 20% increase in productivity, and this was a primary motivation in creating a new language.

**MACHINES THAT FILL MEMORY**

The original designer said that "video games are machines that fill memory". The majority of the time, game programmers are thinking about how to fill memory with huge reams of data in ways that allow the data to be efficiently accessed and processed. Hundreds of megabytes of memory must be moved from the hard disk into main memory, and from there into the video card or the processor cache to be processed and returned back to main memory. Because video game players don’t like to wait, all this must be done as fast as is allowable by laws of our universe. The primary purpose of a programming language is to allow the specification of algorithms to manage data. Language features like garbage collection and templated data streams and dynamic string classes may help the programmer write code faster, but they don’t help the programmer write faster code.

**FRICTION REDUCTION**

Another major design goal of Jai is to reduce friction when programming. Friction happens when the syntax of a language interferes with the programmer’s workflow. For example:
- Java requires that all objects be classes, forcing programmers to put the global variables they need into global classes.
- Haskell requires that all procedures be functions and have no side effects.
- C++’s lambda function syntax is different from its class method syntax, which is itself different from its global function syntax.

Java, Haskell and C++ are examples of what could be called “big agenda” languages, where the languages' idealism (and in C++’s case, its lack of a consistent vision) gets in the programmer’s way. Jai is being designed with a low tolerance for friction, especially when it is unnecessary.

**DESIGN FOR GOOD PROGRAMMERS**

Jai is a language designed for good programmers, not against bad programmers. Languages like Java were marketed as idiot-proof, in that it’s much more difficult for programmers to write code that can hurt them. The Jai philosophy is, if you don’t want idiots writing bad code for your project, then don’t hire any idiots. Jai allows programmers direct access to the sharp tools that can get the job done. Game programmers are not afraid of pointers and manual memory management. Programmers do make mistakes and cause crashes, perhaps even serious ones, but the argument is that the increase in productivity and reduction of friction when memory-safe mechanisms are absent more than make up for the time lost in tracking down errors, especially when good programmers tend to produce relatively few errors.

**PERFORMANCE AND DATA-ORIENTED PROGRAMMING**

If as a programmer you care about user experience (which you should), then you should care about the performance of your program. You should reason about your code’s behavior on the range of machines that you’re shipping on, and design your data and control structures to use that hardware’s capability most efficiently. (Here I’m describing [Mike Acton’s “Data-Oriented Design” methodology](https://www.youtube.com/watch?v=rX0ItVEVjHc).) Programmers who care about the performance of their software on their target hardware are inhibited by programming languages that sit between them and the hardware. Mechanisms like virtual machines and automatic memory management interfere with the programmer’s ability to reason about the program’s performance on the target hardware. Abstractions like RAII, constructors and destructors, polymorphism, and exceptions were invented with the intention of solving problems that game programmers don’t have, and with the result of interfering with the solutions to problems that game programmers do have. Jai jettisons these abstractions so that programmers can think more about their actual problems—the data and their algorithms.
