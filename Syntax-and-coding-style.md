## A tiny taste of the language

At the very first beginning, the Jay language was somewhat similar to C with some funny constructs. Now that is more mature a lot of weird syntaxes started to appear so as a first impact you can get a bit confused.


### Comments
```
// Simple one line comment
/* Multi line comment */
/* A strange /* nested */ comment */ 
```
### Constants
```cpp
ALERT  :: 0xFFAA00;           // An hexadecimal constant
RAW_PI :: 3.1416;             // A floating point constant
ROLE_1 :: "Wizard";           // A static string constant
```
*Style*: prefer using all upper case naming convention;


### Variables

The syntax `name: type = value;` specifies that a variable named `name` is of the type `type` will be assigned the value `value`. It was proposed by [Sean Barrett](https://twitter.com/nothings).

If the `type` is omitted it will be automatically inferred by the compiler.

Some examples:
```cpp

// Unassigned declarations will be initialized to default values (zeroes) unless specified
counter     : int;    // Signed 32 bit integer
key         : s64;    // Signed 64 bit integer
flags       : u8;     // Unsigned 8 bit integer

// Declarations and assignments
counter     : int = 0;                 // Simple signed 32 bits integer with assignment
mode        := 10;                     // Type int automatically inferred by the compiler
area        : float = r * r * RAW_PI;  // Single precision 32 bit floating point
average     := 0.5 * (x+y);            // Another float automatically inferred by the compiler
message     : string = "Hello ";       // A standard native unicode 16 bit char string
name        := "Sailor";               // Type string automatically inferred by the compiler

// Multiple declarations
r1, r2: Quaternion = q(1, 0, 0, 0);    // Declare two quaternions initialized with a default value by a factory function
v1, v2: Vector3 = ---;                 // Declare two 3D vectors both assigned to uninitialized values

```
*Style*: Prefer using all lower case naming convention;

### Procedures
```cpp

// Define a procedure with arguments
do_something :: (what: string){
  printf("I'm doing: %", what); 
}

// Another procedure without arguments
main_loop :: (){
  while !should_exit {
    get_user_input();
    simulate();
    render();
    post_process();
  }
}

```
*Style*: prefer using snake case naming convention for all the compound terms

### Functions
```cpp

// Define a simple function
square :: (val: float) -> float {
  return val * val;
}

// Define a function with multiple unnamed results
circle_area:: (radious: float) -> float, bool {
  return square(radious) * RAW_PI, radious > 0 ;
}

// Define a function with multiple named results
complex_calc:: (a: float, b: float) -> (r1: float, r2: bool) {
  r1 := 0.0;
  r2 := true;
  ...
  
  return r1, r2;
}

```

### Aggregated data type
```cpp

// define a new struct type
Spring :: struct {
  relaxed_length : float; // millimeters
  theta          : float; // N/m
  force          : float; // N
  current_length : float; // mm
}
```
*Style*: prefer using capitalization for the first letter of the user-defined types.

``` cpp
// declare a new spring allocate it on the stack and initialize to zeroes
a_spring : Spring;

// use dot notation to access the fields
a_spring.relaxed_length = 100;

// or use the using keyword
using a_spring {
  theta = 1000.0;
  force = 25;
  current_length = theta / relaxed_length * force + relaxed_lenght; 
}

```

### Collection data types
```cpp

// define a new static array on the stack automatically initialized to zeroes
storage : [50] int;
// assign a value by index
storage[0] = 20;

// define a variable-length array and allocate it on the heap
coefficients: [..] float;
// deallocate at the end of the scope
defer coefficients;

// define a list of constant values
verbs: [] string (:string: "put","get","post","delete");

```
Arrays do not automatically cast to memory pointers as in C. Rather, they are special data structures that contain array size information. Functions can take array types and query for the size of the array.

```cpp
print_int_array :: (a: [] int) {
    n := a.count;
    for i : 0..n-1 {
        print("array[%] = %\n", i, a[i]);
    }
}
```
Retaining the array size information can help developers avoid the pattern of passing array lengths as additional parameters (see [C2x proposal](https://en.wikipedia.org/wiki/C2x)) and assist in automatic bounds checking (see [C’s Biggest Mistake](https://digitalmars.com/articles/b44.html)).

### Constat sets: enumerations
```cpp

to be implemented

```

---
### Navigate 
* [Home](./) 
* [Back: Before starting](./Before-starting) 
* [Next: Reserved words](./reserved-words)

