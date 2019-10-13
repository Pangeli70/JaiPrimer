
# Arbitrary Compile-Time Code Execution

Suppose I want to write a function in C that converts a linear color value to [sRGB](http://en.wikipedia.org/wiki/SRGB). This involves the `pow()` function, which is on the expensive side. We can avoid `pow()` by doing the calculation ourselves instead and distributing the results as part of our program. So we write a table of values and return those.

```cpp
#define SRGB_TABLE_SIZE 256
float srgb_table[SRGB_TABLE_SIZE] = { /* ... values here ... */ }

float linear_to_srgb(float f)
{
    // Find the index in our table for this SRGB value,
    // assuming f is in the range [0, 1]
    int table_index = (int)(f * SRGB_TABLE_SIZE);
    return srgb_table[table_index];
}
```

(_Note:_ The above is bad code, only used for example. For better code, try [stb_image_resize’s sRGB functions](https://github.com/nothings/stb/blob/master/stb_image_resize.h).) So far so good, except how will we get the values for the srgb_table? We can write another small program that outputs values. For example:

```cpp
float real_linear_to_srgb(float f)
{
    if (f <= 0.0031308f)
        return f * 12.92f;
    else
        return 1.055f * (float)pow(f, 1 / 2.4f) - 0.055f;
}

#define SRGB_TABLE_SIZE 256

int main(int c, char* s) {
    printf("float srgb_table[SRGB_TABLE_SIZE] = { ");
    for (int i = 0; i < SRGB_TABLE_SIZE; i++)
        printf("%f, ", real_linear_to_srgb((float)i/SRGB_TABLE_SIZE));
    printf("}\n");
    return 0;
}
```

We can compile this small program, which will output a table of sRGB values, and then we can copy the output into our actual program.

This is a big bucket of problems with it. For example, notice how `SRGB_TABLE_SIZE` is defined twice, once in the actual program and once in the helper program. So we now have to maintain two separate source codes. This can get unwieldy for large programs.

In Jai, the same task looks like this:

```cpp
generate_linear_srgb :: () -> [] float {
     srgb_table: float[SRGB_TABLE_SIZE];
     for srgb_table {
         << it = real_linear_to_srgb(cast(float)it_index / SRGB_TABLE_SIZE)
     }
     return srgb_table;
}

srgb_table: [] float = #run generate_linear_srgb(); // #run invokes the compile time execution

real_linear_to_srgb :: (f: float) -> float {
    table_index := cast(int)(f * SRGB_TABLE_SIZE);
    return srgb_table[table_index];
}
```

The `#run` directive instructs Jai to run the function `generate_linear_srgb()` at compile time. Jai’s compile time function execution runs the command at compile time and returns a table of values, which is then compiled directly into the binary as `srgb_table`. When the program is run, the `generate_linear_srgb()` function no longer exists. Only the table it generated exists, which is used by `linear_to_srgb()`.

The compile-time function execution has very few limitations; in fact, you can run arbitrary code in your code base as part of the compiler. The first demonstration of Jai shows how to run [an entire game as part of the compiler](http://youtu.be/UTqZNujQOlA?t=43m57s), and bake the data from the game into the program binary. (I hope `#run invaders();` is shipped with the language.) The compiler builds the compile-time executed functions to a special bytecode language and runs them in an interpreter, and the results are funneled back into the source code. The compiler then continues as normal.

Here are some examples of things that a compile-time function could do:

- Compile-time asserts
- Run test cases
- Do code style checks
- Dynamically generate code and insert it to be compiled
- Insert build time data
- Download the OpenGL spec and build the most recent gl.h header file
- Contact a build server and retrieve/send build data
- Talk to your Mars probe on Mars and wait for the packets to come back and get a photo of what Mars looks like