
Integrated Build Process
------------------------

All information for building a program is contained within the source code of the program. Thus there is no need for a toolchain or building pipeline with `make` / `link` commands or IDE project files to build a Jai program. 

As a simple example:

```cpp
build :: () {
    build_options.executable_name = "my_program";
    print("Building program '%'\n", build_options.executable_name);
    build_options.optimization_level = Optimization_Level.DEBUG;
    build_options.emit_line_directives = false;

    update_build_options();

    // Jai will automatically build any files included with the #load directive,
    // but other files can also be manually added.
    add_build_file("misc.jai");
    add_build_file("checks.jai");
}

#run build(); // <<------ LOOK HERE !!!!

```

When the program is built, the #run directive runs build() at compile-time. Then `build()` establishes all of the build options for this project. No external build tools are required, all build scripting is done within Jai, and in the same environment of the rest of the code.
