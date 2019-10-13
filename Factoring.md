
Code growth
----------------

All code begins its life in some kind of code block like this before moving on to be used in more general cases. Jai has some special syntaxes that can assist the programmer in moving code from specific cases out into general cases, to facilitate code reuse.

As an example, let’s say you’re writing some code like this:

```cpp
draw_particles :: () {
    view_left: Vector3 = get_view_left();
    view_up: Vector3 = get_view_up();

    for particles {
        // Inside for loops the "it" object is the iterator for the current object.
        particle_left := view_left * it.particle_size;
        particle_up := view_up * it.particle_size;

        // m is a global object that helps us build meshes to send to the graphics API
        m.Position3fv(it.origin - particle_left - particle_up);
        m.Position3fv(it.origin + particle_left - particle_up);
        m.Position3fv(it.origin + particle_left + particle_up);
        m.Position3fv(it.origin - particle_left + particle_up);
    }
}
```

These mesh generation calls are actually a special case of some general quad rendering, so they can be factored out into another function so they can be used in other places. Jai makes this refactoring very straightforward. The first step is to enclose the code in a new scope with a special capture syntax.

```cpp
particle_left := view_left * it.particle_size;
particle_up := view_up * it.particle_size;
origin := it.origin;

[m, origin, particle_left, particle_up] {
    m.Position3fv(origin - particle_left - particle_up);
    m.Position3fv(origin + particle_left - particle_up);
    m.Position3fv(origin + particle_left + particle_up);
    m.Position3fv(origin - particle_left + particle_up);
}
```

(_Disclaimer:_ This step hasn’t been implemented yet. It’s one of the planned features.) The `[m, origin, particle_left, particle_up]` notation is a capture that prevents any object not in the capture from being accessed inside the inner scope of the new bracket. Notice that we had to change `it.origin` to `origin` and add `origin` to the capture list—`it` is not captured and is unavailable inside the inner scope.

Captures help in refactoring code as we’re seeing here but they can also help in other ways. For example, when programmers are moving code from being singlethreaded to multithreaded, captures could enforce that only thread-local data is accessed. Captures are an insurance policy that the code inside the capture only reads or writes the state specified in the capture.

Now we’ve identified all of the parts of our code that depend on external things, so we’ve improved our code’s hygiene and made it easy to pull this code out into its own function. Now we want to continue so that we can use the quad drawing code in other places. So we create a function out of this block capture:


```cpp
particle_left := view_left * it.particle_size;
particle_up := view_up * it.particle_size;
origin := it.origin;

() [m, origin, particle_left, particle_up] {
    m.Position3fv(origin - particle_left - particle_up);
    m.Position3fv(origin + particle_left - particle_up);
    m.Position3fv(origin + particle_left + particle_up);
    m.Position3fv(origin - particle_left + particle_up);
} (); // Call the function
```

Notice how the only change we needed to make was to add the function syntax `()`. The capture remained intact. So we went from a blocked capture to a function with very little effort. Now if we like we can move the vectors to be function parameters:

```cpp
(origin: Vector3, left: Vector3, up: Vector3) [m] {
    m.Position3fv(origin - left - up);
    m.Position3fv(origin + left - up);
    m.Position3fv(origin + left + up);
    m.Position3fv(origin - left + up);
}
```

With parameter names we’re able to change the names of the variables inside the function’s scope to match their new function. Now we can use this function to draw any type of quad, not just particles. The capture retains `m` because it is a global object that doesn’t need to be passed as a parameter. And now we have an anonymous, locally scoped function that can be used in our draw code:

```cpp
draw_particles :: () {
    view_left: Vector3 = get_view_left();
    view_up: Vector3 = get_view_up();

    for particles {
        particle_left := view_left * it.particle_size;
        particle_up := view_up * it.particle_size;

        (origin: Vector3, left: Vector3, up: Vector3) [m] {
            m.Position3fv(origin - left - up);
            m.Position3fv(origin + left - up);
            m.Position3fv(origin + left + up);
            m.Position3fv(origin - left + up);
        } (origin, particle_left, particle_up);  // Call the function with the specified parameters
    }
}
```

Anonymous functions are useful for passing as arguments to other functions, and this syntax makes them easy to create and manipulate. The next step is to give our function a name:

```cpp
draw_quad :: (origin: Vector3, left: Vector3, up: Vector3) [m] {
    m.Position3fv(origin - left - up);
    m.Position3fv(origin + left - up);
    m.Position3fv(origin + left + up);
    m.Position3fv(origin - left + up);
}

draw_quad(origin, particle_left, particle_up);
```

Now we could call it multiple times in the local scope, if we like. But we want to access our quad drawing function from the global scope. Moving the function out of the local scope requires zero changes to the function’s code:

```cpp
draw_quad :: (origin: Vector3, left: Vector3, up: Vector3) [m] {
    m.Position3fv(origin - left - up);
    m.Position3fv(origin + left - up);
    m.Position3fv(origin + left + up);
    m.Position3fv(origin - left + up);
};

draw_particles :: () {
    view_left: Vector3 = get_view_left();
    view_up: Vector3 = get_view_up();

    for particles {
        particle_left:= view_left * it.particle_size;
        particle_up:= view_up * it.particle_size;

        draw_quad(particle_left, particle_up, origin);
    }
}
```

The strength of Jai’s function syntax is that it doesn’t change whether the function is an anonymous function, a local function (i.e. lives inside the scope of another function) a member function of a class or a global function. This is in contrast to in C++, where a local function is called a lambda, and has completely different syntax than a member function, which must have a class name and `::` etc, which is slightly different syntax than a global function which has no class name or `::`. The result is that as code matures and moves from a local context to a global context, the work of refactoring can be done with minimal edits.

Here is Jai’s code maturation process in full:

```cpp
                                 { ... } // Anonymous code block
                       [capture] { ... } // Captured code block
     (i: int) -> float [capture] { ... } // Anonymous function
f :: (i: int) -> float [capture] { ... } // Named local function
f :: (i: int) -> float [capture] { ... } // Named global function
```
