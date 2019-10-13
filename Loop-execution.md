In Jai loops are one of the most interesting features, they are both powerful and concise.

## For Statement
The for loops apply to situations where the number of iterations is known before the execution. So for most cases.

For loops are used widely to iterate over arrays.

An iteration over arrays, somewhat semantically similar to the 'C' style, using indexes is still possible. 

``` cpp

lines: [..] string;               // Declare a variable lenght array of strings
lines = read_lines(file_name);    // Pretend to read the content of a text file 
lines_number := lines.count;      // Arrays contains a field that stores the amount of elements

// Perform N operations iterating over a range of numbers
i := 0;                           // Declare an index variable
// Use a range operator to define a set of numbers to iterate over
for 1..lines_number print_line(lines[i++]);

```

In Jai instead, we can leverage a simple _item_ concept and so it is possible to use the keywords 'it' and 'it_index' to get direct access to the items of the arrays.
This allows extremely coincise and effective syntax avoiding lambdas or high order functions used in other languages.  

``` cpp
ROW_SIZE :: 10;                         // A constant int declaration
row_cells : [ROW_SIZE] int;             // A statically defined array of integers

// Preferred Jai style:
// Iterate over the array using the 'it' keyword
// Here 'it' means 'row_cells[it_index]'
for rows_cells it = random_int(1,100);

// Alternative Jai style:
// Iterate over the array using a renamed item iterator
// Here 'cell' is an alias of the 'it' keyword and still means 'row_cells[it_index]'
for cell: rows_cells cell = random_int(1,100);

// Alternative Jai style:
// Iterate over the array using the 'it_index' keyword
// 'it_index' is a zero based number from the first to the last element of the array
for rows_cells row_cells[it_index] = random_int(1,100);

// Alternative Jai style:
// Iterate over the array using a renamend index item of a range operator
for i: 0..ROW_SIZE-1 row_cells[i]= random_int(1,100);

```
This is possible because in Jai the arrays are data structures that not only store the data but also the number of the contained items. See the [arrays page](arrays) for further details.

### For break / continue
It is possible to interrupt completely an iteration using the `break` keyword.
``` cpp
for entities {
  if need_update(it) break;
  else {
    ...
  }
}
```

Instead, it is possible to skip an iteration using the `continue` keyword.
``` cpp
for entities {
  if it.updated continue;
  else {
    ...
  }
}
```

## While Statement
The while loops apply to situations where the number o iterations depend on external conditions 

``` cpp

```