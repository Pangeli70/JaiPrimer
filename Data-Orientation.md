### WARNING THESE FEATURES AT PRESENT TIME ARE REMOVED FROM THE CURRENT COMPILER

# Data-Oriented Structures

**SOA AND AOS**

Modern processors and memory models are much faster when spatial locality is adhered to. This means that grouping together data that is modified at the same time is advantageous for performance. So changing a struct from an array of structures (AoS) style:

```cpp
struct Entity {
    Vector3 position;
    Quaternion orientation;
    // ... many other members here
};

Entity all_entities[1024]; // An array of structures

for (int k = 0; k < 1024; k++)
    update_position(&all_entities[k].position);

for (int k = 0; k < 1024; k++)
    update_orientation(&all_entities[k].orientation);
```

to a structure of arrays (SoA) style:

```cpp
struct Entity {
    Vector3 positions[1024];
    Quaternion orientations[1024];
    // ... many other members here
};

Entity all_entities; // A structure of arrays

for (int k = 0; k < 1024; k++)
    update_position(&all_entities.positions[k]);

for (int k = 0; k < 1024; k++)
    update_orientation(&all_entities.orientations[k]);
```

can improve performance a great deal because of fewer cache misses.

However, as programs get larger, it becomes much more difficult to reorganize the data. Testing whether a single, simple change has any effect on performance can take the developer a long time, because once the data structures must change, all of the code that acts on that data structure breaks. So Jai provides mechanisms for automatically transitioning between SoA and AoS without breaking the supporting code. For example:

```cpp
Vector3 :: struct {
    x: float = 1;
    y: float = 4;
    z: float = 9;
}

v1 : [4] Vector3;     // Memory will contain: 1 4 9 1 4 9 1 4 9 1 4 9

Vector3SOA :: struct SOA {
    x: float = 1;
    y: float = 4;
    z: float = 9;
}

v2 : [4] Vector3SOA;  // Memory will contain: 1 1 1 1 4 4 4 4 9 9 9 9
```

Getting back to our previous example, in Jai:

```cpp
Entity :: struct SOA {
    position : Vector3;
    orientation : Quaternion
    // .. many other members here
}

all_entities : [4] Entity;

for k : 0..all_entities.count-1
    update_position(&all_entities[k].position);

for k : 0..all_entities.count-1
    update_orientation(&all_entities[k].orientation);
```

Now the only thing that needs to be changed to convert between SoA and AoS is to insert or remove the `SOA` keyword at the struct definition site, and Jai will work behind the scenes to make everything else work as expected.