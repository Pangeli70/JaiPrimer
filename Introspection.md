
# Run-Time Type Information

Jai stores a table of all type information in the data segment of each compiled program. It can be examined like this:

```cpp
for _type_table {
    // it is the iterator, it is the Type being examined. it_index is the iteration index, it is an integer
    print("%:\n", it_index);
    print("  name: %\n", it.name);
    print("  type: %\n", it.type); // type is an enum, INTEGER, FLOAT, BOOL, STRUCT, etc
}
```

Full introspection data is available for all structs, functions, and enums. For example, a procedure may look something like this:

```cpp
print("% (", info_procedure.name);
for info_procedure.argument_types {
    print_type(it);
    if it_index != info_procedure.argument_types.count-1 then print(", ");
}
print(") ->");
print_type(info_procedure.return_type);
```

The preceding code could print something like `get_name(id : uint32) -> string`. An enum can be examined like this:

```cpp

Hello :: enum u16 {
    FIRST,
    SECOND,
    THIRD = 80,
    FOURTH,
}

for Hello.names {
    print("Name: % value: %\n", Hello.names[it_index], Hello.values[it_index]);
}
```

RRTI data such as this can be used to write serialization procedures, commonly used e.g. in network replication of entities and save game data. Current C/C++ methods for this involve heavy use of operator overloading and preprocessor directives.
