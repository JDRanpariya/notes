# Arrays

Following line declares an array of 100 int objects
 - `int my_array[100];`

## Array Initialization
 - `int array[] = { 1, 2, 3, 4 };`
 - length of the array can be inferred from the no. of elements in the braces at complile time.
 
## Accessing Array Elements
 - zero based indexing
 - `printf("%d", array[3]);` will print 4

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
   - `enum class Race {Dinan, Teklen, Ivyn, Julian, Aidan};`
   - that declares an enum class Race that can take one of the 5 values.
   - To initialize enum var to value use name of type followed by :: and the desired value
    - `Race langobard_race = Race::Aidan;`
  - Switch Statments
    > It transfers control to one of several statements depending on the value of a condition, which evaluates to either an integer or enumeration type.
    > default kyword denotes the default condition.
    - general syntex
     `switch (condition) {
        case (case-a): {
            // Handle case a here
        } break;
        case (case-b): {
            // Handle case b here
        } break;
        default: {
            // Handle default case here
        }
       }`
   - Using switch statement with an Enumeration Classes
     ` int main(){
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
       } `
 - Classes
   > More fully featured types that give you glexibility to pair data and func.
   - also called POD (Plain-Old-Data Classes)
   `struct Book {
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
> In c++ you achieve encapsulation by adding methods and access controls to class definations.
 ### Methods
 - Methods are member functions.
 - They create an explicit connection among a class, it's data members and some code.
 `struct clockOfTheLongNow {
    int year;

    void add_year() {
        year++;
    }
 };`
 ### Access Controls
  > Access Controls restrict class-member access.
  - Public and private are two major AC.
  `struct ClockOfTheLongNow {
void add_year() {
    year++;
}
bool set_year(int new_year) { // setter method to set year 
if (new_year < 2019) return false; 
    year = new_year;
    return true;
}
int get_year() { // getter method to get year
    return year;
}
private: 
    int year;
};`
 #### The Class Keyword
  > You can replace struct with class keyword which declares members private by default.
 #### Initializing Members
  - uninitialized variables can contain random data
  - so after saying `clockOfTheLongNow clock;` we need to make sure its not less then 2019.
  - to guarantee that year is never less than 2019 under any circumstances. Such a
    requirement is called a class invariant: a feature of a class that is always true
    (that is, it never varies).
  - it's better to employ constructor here.
    > Constructors initialize objects and enforce class invariants from the very beggining of an objects life.

 ### Constructors
  > This are spacial methods with special declarations & it doesn't state return type.
  `struct ClockOfTheLongNow {
    ClockOfTheLongNow() {  // constructor, method name same as class name
            year = 2019; 
    }
        --snip--
   };`

 ### Initialization
 - Initializing a Fundamental Type to zero (4 Ways)
   `int a = 0; // Initialized to 0 using literal
    int b{};   // Initialized to 0 braced initialization
    int c = {};// Initialized to 0
    int d;     // Initialized to 0 (may be)` // don't use this (random value)
 - Initializing a Fundamental Type to an Arbitary Value
   `int e = 12; // Initialized to 42
    int f{23};  // Initialized to 23
    int g = {2};// Initialized to 2
    int h(32);  // Initialized to 32`
 - Initializing POD'same
   - `clockOfTheLongNow initialized_pod1{};
      clockOfTheLongNow initialized_pod2 = {}
      clockOfTheLongNow initialized_pod3 = {23, "hello"}

      clockOfTheLongNow initialized_pod = 0; // expressly forbidden in language rules`

 - Initializing Fully Featured Class
   - They always gets Initialized with default constructor
   - if you say clockOfTheLongNow(); it will return an object of type clockOfTheLongNow.
 - Narrowing Conversions ??
 ### General Rule of Initialization to make it simple 
   - use braced initiazation everywhere

 ### Destructor
   > An objects distructor is it's cleanup function. it's invoked before an object is destroyed.
   - use ~ to declare destructor
   `#include <cstdio>
	struct Earth {
			~Earth() { // Earth's destructor
				printf("Making way for hyperspace bypass");
		}
	}
	`
    - It's optional
    - If you implement one, it must not take any argument
    - usage: flusing network sockets, freeing dynamic objects and releasing file handles
    - If you don’t define a destructor, a default destructor is automatically
      generated. The default destructor’s behavior is to perform no action
