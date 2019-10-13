
Polymorphic subroutines
----------------------

Jai’s primary polymorphism mechanism is at the function level and is best described with an example.

```cpp
sum :: (a: $T, b: T) -> T {
    return a + b;
}

f1: float = 1;
f2: float = 2;
f3 := sum(f1, f2);

i1: int = 1;
i2: int = 2;
i3 := sum(i1, i2);

x := sum(f1, i1);

print("% % %\n", f3, i3, x); // Output is "3.000000 3 2.000000"
```

When `sum()` is called, the type is determined by the `T` which is preceded by the `$` symbol. In this case, `$` precedes the `a` variable, and so the type `T` is determined by the first parameter. So, the first call to `sum()` is float + float, and the second call is int + int. In the third call, since the first parameter is float, both parameters and the return value become float. The second parameter is converted from int to float, and the variable `x` is deduced to be float as well.

**THE ANY TYPE**

Jai has a type called `Any`, which any other type can be implicitly casted to. Example:

```cpp
print_any :: (a: Any) {
    if a.type.type == Type_Info_Tag.FLOAT
        print("a is a float\n");
    else if a.type.type == Type_Info_Tag.INT
        print("a is an int\n");
}
```