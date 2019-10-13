Memory Management
-----------------

Jai does not and will never feature garbage collection or any kind of automatic memory management.

**STRUCT POINTER OWNERSHIP**

Marking a pointer member of a struct with `!` indicates that the object pointed to is owned by the struct and should be deleted when the struct is deallocated. Example:

```cpp
node :: struct {
    owned_a : !* node = null;
    owned_b : !* node = null;
}

example: node = new node;
example.owned_a = new node;
example.owned_b = new node;

delete example; // owned_a and owned_b are also deleted.
```

Here, `owned_a` and `owned_b` are marked as being owned by `node`, and will be automatically deleted when the node is deleted. In C++ this is accomplished through a `unique_ptr<T>`, but Jai considers this the wrong way to do it, because the template approach now masks the true type of the object. A `unique_ptr<node>` is no longer a `node`—it’s a `unique_ptr` masquerading as a `node`. It’s preferable to retain the type of `node*`, and retain the properties of `node*`-ness that go along with it, because we don’t really actually care about `unique_ptr` for its own sake.

**LIBRARY ALLOCATORS**

… this section is not written yet! Sorry. (Jai provides mechanisms for managing the allocations of an imported library without requiring work from the library writers.)

[//]: # (Explicit Performance Control)

**INITIALIZATION**

Member variables of a class are automatically initialized.

```cpp
Vector3 :: struct {
    x: float;
    y: float;
    z: float;
}

v : Vector3;
print("% % %\n", v.x, v.y, v.z); // Always prints "0 0 0"
```

You can replace these with default initializations:

```cpp
Vector3 :: struct {
    x: float = 1;
    y: float = 4;
    z: float = 9;
}

v : Vector3;
print("% % %\n", v.x, v.y, v.z); // Always prints "1 4 9"

va : [100] Vector3;                                 // An array of 100 Vector3
print("% % %\n", va[50].x, va[50].y, va[50].z); // Always prints "1 4 9"
```

Or you can block the default initialization:

```cpp
Vector3 :: struct {
    x: float = ---;
    y: float = ---;
    z: float = ---;
}

v : Vector3;
print("% % %\n", v.x, v.y, v.z); // Undefined behavior, could print anything
```

You can also block default initialization at the variable declaration site:

```cpp
Vector3 :: struct {
    x: float = 1;
    y: float = 4;
    z: float = 9;
}

v : Vector3 = ---;
print("% % %\n", v.x, v.y, v.z); // Undefined behavior, could print anything

va : [100] Vector3 = ---;
print("% % %\n", va[50].x, va[50].y, va[50].z); // Undefined behavior, could print anything
```

By explicitly uninitializing variables rather than explicitly initializing variables, Jai hopes to reduce cognitive load while retaining the potential for optimization.
