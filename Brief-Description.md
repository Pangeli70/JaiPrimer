In short, Jai could be described as a data-oriented modern replacement for C alternative to C++ and the OOP culture.

### Coherent semantics and syntax
All reserved words, symbols, and constructs are meant to get overall consistency and clarity of intent, even if using a simple and terse syntax.

### Metaprogramming through compile-time code execution
Any function can run at compile time using special compiler directives (eg. `#run`) This allows the programmer to build entire portions of the code during compilation, even in nested cycles of iteration getting rid of preprocessors and macro expansion. 

### Out of order compilation
All declarations can be made in any order, the compiler figures out the missing dependencies without the need of header files, even if portions of the code will be available after further cycles of metaprogramming generation.

### Compilation speed
The compiler target throughput is 1,000,000 raw lines per second. This feature alone will reduce considerably the overall amount of time spent in developing the code, with several other benefits.

### Meaningful and contextualized error messages
The compiler gives contextualized, clear, concise and accurate error messages and also hints and possibly suggestions, to help the programmer to fix the syntax errors easily.

### Iterative code factoring
The language syntax facilitates code evolution by making it easy to generalize the code via progressive refinement, moving it from function scope → to a local block → to a local "private" function → finally to a global "public" function that can be used everywhere.

### Integrated build process
No use of external or additional tools: the build process and its parameters are specified in the source code itself, via normal functions that the compiler understands.

### Data-oriented design features
The language is aimed toward efficient bulk data manipulation, and transformation of data streams, instead of focusing on data ownership abstractions, typical of so-called OOP languages. 

### Introspection and run-time type information
Static type information for every data type is available at runtime and can be used conveniently by the programmer to implement features available in other dynamically typed languages.

### Polymorphic procedures
Polymorphism at the function level allows the programmer to apply data manipulation algorithms to different data sets or data streams.

### Low-level memory management tools
Total control over memory allocation, automatic ownership management, no automatic garbage collection, minimization of deallocation and heap fragmentation using efficient memory pool operations.

### Explicit but flexible control over low-level optimization and performance
Explicit control over things like inlining, bounds checking, and initialization.

### Code visualization and debugging tools
The compiler gives advanced code statistics using also a graphic representation of the produced machine code. This data can be used both by debuggers and profiler tools. 


---
### Navigate 
* [Home](./) 
* [Back: Disclaimers](./Disclaimers) 
* [Next: Raw material](./Raw-material)