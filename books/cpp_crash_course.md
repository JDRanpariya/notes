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
 - Enumerations
  > the values that an enum can take are restricted to a set of possible values.
  - enum class Race {Dinan, Teklen, Ivyn, Julian, Aidan};
  - that declares an enum class Race that can take one of the 5 values.
  - To initialize enum var to value use name of type followed by :: and the desired value
    - Race langobard_race = Race::Aidan;
  - Switch Statments
   > It transfers control to one of several statements depending on the value of a condition, which evaluates to either an integer or enumeration type.
   > default kyword denotes the default condition.
   - general syntex
    - switch (condition) {
        case (case-a): {
            // Handle case a here
        } break;
        case (case-b): {
            // Handle case b here
        } break;
        default: {
            // Handle default case here
        }
      }
   - Using switch statement with an Enumeration Classes
    - `int main(){
        Race race = Race::Dinan;

        switch(race) {
        case Race::Dinan:{
            printf("you work hard.");
        } break;
        case Race::Teklan: {
            printf("You are very brave");
        } break;
        case Race::Ivyn: {
            printf("You are a great leader.");
        } break;
        case Race::Aidan: {
            printf("What an enigma");
        } break;
        default: {
            printf("Error: unknown race!");
        }
        }
      }`
 - Classes
  > More fully featured types that give you glexibility to pair data and func.
  - also called POD (Plain-Old-Data Classes)
  - `struct Book {
       char name[256];
       int year;
       int pages;
       bool hardcover;
    }`
    - You can access members of the var using the dot operator (.)
        `Book neuromancer;
         neuromancer.pages=324;
         printf("%d", neuromancer.pages)`
 - Unions
  > A boutique user-defined type. All members share the same memory location. easy to misuse.
  - avoid using unions ( causes data corruption easily )

## Fully Featured C++ Classes

