## Acronyms
- OOP - Object-oriented Design
- [DOD](https://en.wikipedia.org/wiki/Data-oriented_design) - Data-Oriented Design
- TDD - Test-Driven Design
- [RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization) - Resource Acquisition Is Initialization
- [RTTI](https://en.wikipedia.org/wiki/Data-oriented_design) - Run time type information 
- AOS - Array of structures
- SOA - Structure of arrays

## Terminology

### Factoring
Evolution of the code through iterative modifications, compilation, quick testing 

### Refactoring
Modification of the code aimed to get better performance by using different algorithms. In other languages or in some code editors means contextual renaming through smart search & replace.

### Type inference [->](https://en.wikipedia.org/wiki/Type_inference)
The capability of the compiler to infer the type of a variable by its content or its assignment

### Introspection [->](https://en.wikipedia.org/wiki/Reflection_(computer_programming))
The capability of getting data type information at runtime.

### Reflection
Same as introspection used often in languages like C#, Java or JS.

### Metaprogramming [->](https://en.wikipedia.org/wiki/Metaprogramming)
The capability of the software to rewrite itself by the means of the compiler.

### Deferred execution
Execution in stacked reverse order at the end of the current scope.

### Scope [->](https://en.wikipedia.org/wiki/Scope_(computer_science))
It is a block of code where the association between names and entities (variables, procedures) is defined. Scopes can be nested in many levels of depth inside the general global scope of the application. The concept is used to identify potential naming collisions. 

### Procedure [->](https://en.wikipedia.org/wiki/Subroutine)
A reusable block of code that has an entry point, that accepts arguments, performs a task and has an exit point.

### Function
A procedure that after the execution returns some values. In Jai a function can return multiple values.

### Pure function
A function that has no side effects, and performs its task operating only on its arguments, without effecting any other data from outer scopes.

### Constructor
The special procedure used in OOP languages for initialization of data structures (classes) and allocation of resources (see RAII).

### Destructor
A special procedure in OOP languages used for deletion of data structures (classes) and deallocation or release of resources.

### Inheritance
In OOP languages it is the extension of a data structure and its method, by the creation of a derived more specialized version.

### Composition
In data management is meant as the extension of a data structure by aggregation/sum of different data structures. In functional languages is used to describe the composition of simple functionalities to get more complex algorithms.

### Execution context
In Jai it is a special data structure that holds a reduced version of the global scope with preallocated utility data pools.

### Heap [->](https://en.wikibooks.org/wiki/Introduction_to_Programming_Languages/Heap)
Is the memory that the OS gives to the application to store the dynamically allocated data.

### Memory pool [->](https://en.wikibooks.org/wiki/C%2B%2B_Programming/Memory_Management_Techniques)
A contiguous block of memory allocated once and used as a cache or buffer by many other smaller data structures.

### Allocator [->](https://en.wikibooks.org/wiki/Optimizing_C%2B%2B/Writing_efficient_code/Allocations_and_deallocations#Allocating_many_small_objects)
A specialized procedure used to allocate memory from a memory pool instead than form the heap. In Jai allocators can be associated with the execution context.




 
