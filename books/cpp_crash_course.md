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

# Chapter 3 - REFERENCE TYPES
> Reference types store the memory addresses of objects.This type enable efficient programming, and many elegant design patterns feature them.
> Pointers and References along with this, const, and auto

## Pointers
 > It is a fundamental mechanism used to refer to memory addresses.
 - * is an address-of operator
 - declaration: `int* my_ptr;`
 - format specifier: `%p`
 - void pointers & std::byte pointers

## Addressing Variables
 - & is used to get addresse of a variables
 `#include <cstdio>
  int main() {
      int num{};
      int *num_addr = &num; // num_addr has address of variable num
  }`
  - each time you print &num it's value will be different due to ADDRESS SPACE LAYOUT RANDOMIZATION

## Dereferencing Pointers
 > * is a unary operator that accesses the object to which a pointer refers.
 - Given an address, you can obtain the object residing there
 `int main() {
     *num_addr = 3;
     printf("Value at num_addr: %d", *num_addr);
 }`
 - above will print 3 as we changed value of object residing at address stored in num_addr
 
## Member-of-Pointer Operator
 - It (->) performs two simultaneous operations:
   1. It dereference a pointer
   2. It accesses a member of the pointed-to object
 `ClockOfTheLongNow clock;
  ClockOfTheLongNow* clock_ptr = &clock;
  clock_ptr->set_year(2020); // same as (*clock_ptr).set_year(2020)`

## Pointers and Arrays
 > Pointers share several characteristic with arrays. Pointers encode location. Arrays encode the location and length of contiguous objects.
 > Also, array will dacay into pointer. A decayed array loses length info and converts to a pointer to the array's first element.
 `int key[]{3, 6, 9}
  int* key_ptr = key; // Points to 3`
 - Handling Decay // watch some video
 - Pointer Arithmetic
     - `key* 2nd_key_ptr = &key[1];
        key* 2nd_key_ptr = key + 2`
## Pointers are Dengerous
 - It's not possible to convert pointer to array
 ### Buffer Overflows
  `#include <cstdio>
   int main() {
       char lower[] = "abc?e";
       char upper[] = "ABC?E";
       char* upper_ptr = upper;  // Equivalent: &upper[0]

       lower[3] = 'd';  // lower now contains a b c d e \0
       upper_ptr[3] = 'D'; // upper now contains A B C D E \0

       char letter_d = lower[3];  // letter_d equals 'd'
       char letter_D = upper_ptr[3]; // letter_D equals 'D'

       printf("lower: %s\nupper: %s", lower, upper); 

       lower[7] = 'g';  // Super bad. You must never do this.
   }
   lower: abcde x
   upper: ABCDE
   The time is 2:14 a.m. Eastern time, August 29th. Skynet is now online.`
   - Finally, you make a major boo-boo by writing out-of-bounds memory y.
     By accessing the element at index 7 x, you’ve gone past the storage allotted
     to lower. No bounds checking occurs; this code compiles without warning.
     At runtime, you get undefined behavior. Undefined behavior means the
     C++ language specification doesn’t prescribe what happens, so your program
     might crash, open a security vulnerability, or spawn an artificial general
     intelligence
 - Connection between Breckets and pointer arithmetics

## void Pointers and std::byte Pointers
 ### void pointers
  - Sometimes the pointed-to type is irrelevant. In such situations, we use void pointer void*.
  - void pointers have important restrictions
    - you can't dereference void* ( bcoz the pointed to type has been erased )
    - c++ forbids void pointer arithmetic

 ### std::byte pointer
  - It's used when you want to interact with raw memory at the byte level
  - i.e. low-level operations like copying raw data between files
    and memory, encryption, and compression
  - You can't use void* because bit-wise and arithmetic operations are disabled
 
## nullptr and Boolean Expressions
 - pointers have special literal value, nullptr
 - nullptr doesn’t point to anything
 - pointers have an implicit conversion to bool
   1. any value that is not nullptr converts implicitly to true
   2. whereas nullptr converts implicitly to false.
   3. useful when a function returning a pointer ran successfully

## References
 > References are safer & more convenient versions of pointers
 - declared with & operator
   `ClockOfTheLongNow& clock`
 - References can't be assigned to null ( easily ) & can't be reseated( or reassigned )
 - The syntax for dealing in references is much cleaner than for pointers.
   Rather than using the member-of-pointer and dereference operators, you
   use references exactly as if they’re of the pointed-to type.
   `
   #include <cstdio>
   struct ClockOfTheLongNow {
       --snip--
       
   };
   void add_year(ClockOfTheLongNow&u clock) {
       clock.set_year(clock.get_year() + 1);  // No deref operator needed
       
   }
   int main() {
       ClockOfTheLongNow clock;
       printf("The year is %d.\n", clock.get_year()); 
       add_year(clock);  // Clock is implicitly passed by reference!
       printf("The year is %d.\n", clock.get_year()); 
       
   }

   `
## Usage of Pointers and References 
 > Pointers and references are largely interchangeable, but both have tradeoffs.
   If you must sometimes change your reference type’s value—that is,
   if you must change what your reference type refers to—you must use a
   pointer. Many data structures (including forward-linked lists, which are
   covered in the next section) require that you be able to change a pointer’s
   value. Because references cannot be reseated and they shouldn’t generally
   be assigned to nullptr, they’re sometimes not suitable.

 ### Forwarded-Linked Lists: The Cannonical Pointer-Based Data Structure
  `struct Element {
      Elemnet* next{}; // -> nullptr
      void insert_after(Element* new_element) {
          new_element->next = next;
          next = new_element;
      }
      char prefix[2];
      short operating_number;
  };`

 ## Employing References
   - ??

 ## this Pointers
  > Within method definitions, you can access the current object using the this pointer
 `struct Element { 
         Elemnet* next{}; // -> nullptr
         void insert_after(Element* new_element) {
             this->next = next; // done in one line
         }
          char prefix[2];
          short operating_number;
      };`

 ## const Correctness
  > const means "I promise not to modify". It prevents unintended modifications of member variables by that class or function.
  - const Arguments
    - A const pointer or reference provides you with an efficient mechanism to pass an object into a function for read-only use.
    ` void petruchio(const char* shrewu) {
        printf("Fear not, sweet wench, they shall not touch thee, %s.", shrewv);
        shrew[0] = "K"; w // Compiler error! The shrew cannot be tamed.
     }`
     - you can read from shrew but attempting to write to it will result in compiler error
  - const Methods
    - Marking a method const communicates that you promise not to modify the current object’s state within the const method
    `struct ClockOfTheLongNow {
            --snip--
            int get_year() const {
            return year;
        }
        private:
        int year;
     };`
  - const Menber Variables
    - const member variables can't be modified after their initialization
    - ??

  - Member Initializer Lists
    - Member initializer lists are the primary mechanism for initializing class members
    > You should order the member initializers in the same order they appear in the class definition, because their constructors will be called in this order.
    - ??

 ## auto Type Deduction
  > As a strongly typed language, C++ affords its compiler a lot of information. When you initialize elements or return from functions, the compiler can divine type information from context. The auto keyword tells the compiler to perform such a divination for you, relieving you from inputting redundant type information
  ### Initialization with auto
    > In most cases, the compiler can determine the correct type of an object using the initialization value
    ` auto the_answer { 42 }; // int
      auto foot { 12L }; // long
      auto rootbeer { 5.0F }; // float
      auto cheeseburger { 10.0 }; // double
      auto politifact_claims { false }; // bool
      auto cheese { "string" }; // char[7]`

  ### auto and Reference Types
   - It's common to add modifiers like &,* and const to auto.
       `
       auto year { 2019  }; // int
       auto& year_ref = year; // int&
       const auto& year_cref = year; // const int&
       auto* year_ptr = &year; // int*
       const auto* year_cptr = &year; // const int*

       `

  ### auto and Code Refactorings
  - ??

# Chapter 4 - Objects life Cycle
