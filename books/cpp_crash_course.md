# Arrays

Following line declares an array of 100 int objects
 - int my_array[100];

## Array Initialization
 - int array[] = { 1, 2, 3, 4 };
 - length of the array can be inferred from the no. of elements in the braces at complile time.
 
## Accessing Array Elements
 - zero based indexing
 - printf("%d", array[3]); will print 4

## No. of Elements in Array
 - sizeof(array) will give size in bytes
 - use sizeof(array) / sizeof(int) to get the no. of elements
 - best practise: use std::size func from <iterator> header
 
## C-Style Strings
 - also called null terminated string
 - has zero-byte appended to its end ( to indicate end of string )
 - String Literals
   - use "YOUR STRING HERE"
   - for unicode use u"\u4e78"
 
# User-Defined Types
> types that user can define. There are three broad categories.
