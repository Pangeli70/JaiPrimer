The documents in this page come from the original BSVino's files but now are obsolete and need heavy rearrangement. 
ASAP this text will be updated and moved from here.

---
### Navigate 
* [Home](./) 
* [Back: Brief description](./Brief-description) 
* [Next: Before starting](./Before-starting)

---


Jai Language Features
=====================




**BAKING**

… this section is not written yet! Sorry. (The `#bake` directive emits a function with a combination of arguments baked in. For example, `#bake sum(a, 1)` becomes equivalent to `a += 1`.)




Other Cool Stuff
----------------

Things that C/C++ should have had a long time ago:

- Specific data types for 8, 16, and 32 bit integers
- No implicit type conversions
- `.` operator for both struct membership and pointer dereference access—no more `->`
- A `defer` statement, [similar to that of Go](http://blog.golang.org/defer-panic-and-recover)

Planned
-------

Here’s a shortlist of planned features to be added to Jai.

- Captures
- LLVM integration
- Automatic versioning (see below)
- A better concurrency model
- Named argument passing
- A permissive license

Not Planned
-----------

Jai will not have:

- Smart pointers
- Garbage collection
- Automatic memory management of any kind
- Templates or template metaprogramming
- RAII
- Subtype polymorphism
- Exceptions
- References
- A virtual machine (at least, not usually—see below)
- A preprocessor (at least, not one resembling C’s—see below)
- Header files

If it sounds odd to you that Jai is a modern high-level language but does not have some of the above features, then consider that Jai is not trying to be as high-level as Java or C#. It is better described as trying to be a better C. It wants to allow programmers to get as low-level as they desire. Features like garbage collection and exceptions stand as obstacles to low-level programming.

---


Proposed Features
-----------------

These are a few proposed features that have not been implemented yet. To my knowledge they’re not yet in the language. Syntax is preliminary and likely to change.

- Joint Allocations:

```cpp
Mesh :: struct {
    name: string;
    filename: string;
    flags: uint;

    positions: [] Vector3;
    indices: [] int;        @joint positions
    uvs: [] Vector2;        @joint positions
}

example_mesh: Mesh;
example_mesh.positions.reserve(positions: num_positions,
                               indices: num_indices,
                               uvs: num_uvs);
```

Here we want to avoid multiple memory allocations, so we have the compiler do a joint allocation between positions, indices, and uvs, and divide the memory up accordingly. Currently this is done manually in C, and is prone to errors.

- Optional Types:

```cpp
do_something :: (a: Entity?) {
    a.x = 0; // ERROR!
    if (a) {
        a.x = 0; // OK
    }
}
```

The idea here is to prevent one of the most common causes of crashes, null pointer dereferencing. The ? in the above code means that we don’t know whether or not the pointer is null. Trying to dereference the variable without testing to see if it is null would result in a compile-time error.

- Automatic Versioning:

```cpp
Entity_Substance :: struct { @version 37
    flags: int;
    scale_color: Vector4;   @15
    spike_flags: int;       @[10, 36]
}
```

Here we are providing markup for our data structures that indicate to the compiler what version of the struct each member was present in. These versioning schemes would be used as part of an automatic serialization/introspection interface, but there are no details on that, other than that the language should have some capability of introspection.


---

- Other stuff:
Compilation keyword #bake to specialize polymorphic functions.
A polymorphic function can contain also 'internal' polymorphic type but they can only be used after 'baking' them.

Compilation keyword #modify is used to make constraints/transformations on polymorphic types.
	For example, it allows to define default output polymorphic type, make only one implementation functions for different type u8..32-->u64, complex mapping to reduce the number of generated functions
	NdT: Powerful, but can be used to build function difficult to understand. It uses parameters names as input.
	
Compilation keyword #body_text takes the types of the parameters, then return a string containing the body of the function 
It's planned to have another keyword #body_if for 'inline' compile-time code generation.

#bake_values: a compile time specialization of some function with some (or all) parameters hardcoded.
	Useful to control inlining, somewhat duplicate (force) inline, but easier to use with functions with lots of arguments.
	
$$: an autobaker for function parameters prefixed by $$ and called with literals (currently no analysis to check if the parameter is known at compile time).

End of new features, demonstration of map which shows 'high-levelness' of Jay, but requires to free the allocated memory or there is a memory leak (no GC).
And of map taking an allocator param which allows usage of the stack (faster than heap) for 'inline map'.

In the Q&A video, Blow think that 'libraries' will be pre-parsed code but not binary, to allow these features working.

04/08/2015 Demo: Bounds check, here strings, overloading. [renox, I didn't have the patience to listen to the full Q&A]

* Array Bound Checking (ABC):
By default arrays(both SoA and AoS) and strings are bound checked, for optimization there is a 'no array bound checking' directive: #no_abc (which works either on a statement or on a block),
you can also disable globally ABC, or enforce always ABC (ignoring the #no_abc directive).

SoA pointers are also bound checked as they're 'fat pointers' aka arrays.


* Here strings:
```
# string <end keyword>
...
<end keyword>
```
Currently no indentation support and the <end keyword> must be at the beginning of the line.
Strings are Unicode strings. Can be empty.

* overloaded function:
Overloading works as usual (and also with 'inheritance': Jai 'using' feature).
One main improvement: with integer literals, the smaller int type which can support the literal is called.
Works with multiple parameters.
If there are several possible overload with the same level of conversion, it's a compilation error.
Integer conversion are preferred to float conversion.

There are 'surprising' features related to overloading on which JB ask feedback:
1) overloading is scoped: if you can find a match in the local scope, it is selected, even if there is another better match in the outside scope
baz :: (a: u8) { ... }
{
    baz :: (a: u16) { ... }
    baz(100) // this use the u16 version.
}

2) overloading only work on constant function definition (not on functions pointers, lambda).

3) overloading induce a 'file scope'? [renox. I didn't catch this point]

In the Q&A: parametrized type cannot be overloaded currently.







