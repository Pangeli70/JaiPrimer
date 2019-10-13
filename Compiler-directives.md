
## Compiler

|Directive         | Meaning
|---               |---
| #compiler        | ...
| #complete        | ...
| #expand          | ...
| #foreign         | Declare something coming from an external C obj or DLL compatible library
| #IF              | Entry point for conditional build
| #import          | Import a Library file
| #insert          | ...
| #intrinsic       | Use the intrinsic version of the procedure based on CPU specific instruction.
| #load            | Load another Jai file
| #must            | ...
| #poke_name       | ...
| #run             | Run a procedure at compile time
| #scope_file      | The declarations in the following block are restricted to the current file
| #through         | Used in switch-like statements

## Game engine / Game editor
Game engine directives for the game editor connected to the fields of entities data structures

|Directive         | Meaning
|---               |---
| @NoSerialize     | The field won't be saved in the level file
| @Vn              | Where n is a number. Related to the Entity version.
| @Vn-m            | Where n and m are numbers. Related to the Entity version.
| @Pid             | Unique identifier of the entity 
| @DoNotDisplay    | By default the loaded entity won't be displayed


---
### Navigate 
* [Home](./) 
* [Back: Symbols](./Symbols)
* [Next: ...]()