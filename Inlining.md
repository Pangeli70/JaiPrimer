## Iniline optimization control

```cpp
test_a :: () { /* ... */ }
test_b :: () inline { /* ... */ }
test_c :: () no_inline { /* ... */ }

test_a(); // Compiler decides whether to inline this
test_b(); // Always inlined due to "inline" above
test_c(); // Never inlined due to "no_inline" above

inline test_a(); // Always inlined
inline test_b(); // Always inlined
inline test_c(); // Always inlined

no_inline test_a(); // Never inlined
no_inline test_b(); // Never inlined
no_inline test_c(); // Never inlined
```

Additionally, there exist directives to always or never inline certain procedures, to make it easier to inline or avoid inline conditionally depending on the platform.

```cpp
test_d :: () { /* ... */ }
test_e :: () { /* ... */ }

#inline test_d    // Directive to always inline test_d
#no_inline test_e // Directive to never inline test_e
```