# 42-C-for-Embedded-systems

> C is quirky, flawed, and an enormous success. — Dennis Ritchie

10 Best Questions for Would-be Embedded Programmers.  
(Very entertaining to read and study outside of a interview environment.)

# Preprocessor Questions

## Question 1
Using the #define statement, how would you declare a manifest constant that
returns the number of seconds in a year? Disregard leap years in your answer.  

## Question 2
Write the standard MIN macro. That is, a macro that takes two arguments
and returns the smaller of the two arguments.  

## Question 3
What is the purpose of the preprocessor directive #error?

# Infinite loops

## Question 4
Infinite loops often arise in embedded systems. How does one code an infinite
loop in C?

## Question 5
Using the variable a, write down denitions for the following:
a) An integer  
b) A pointer to an integer  
c) A pointer to a pointer to an integer  
d) An array of ten integers  
e) An array of ten pointers to integers  
f) A pointer to an array of ten integers  
g) A pointer to a function that takes an integer as an argument and returns
an integer  
h) An array of ten pointers to functions that take an integer argument and
return an integer  

## Question 6
What are the uses of the keyword static?  

## Question 7
What does the keyword const mean?

## Question 7.1
What do the following incomplete declarations mean? 
```C
const int a ;
int const a ;
const int ∗a ;
int ∗ const a ;
int const ∗ a const;
```

## Question 8
What does the keyword volatile mean? Give three different examples of its use.

## Question 8.1
(a) Can a parameter be both const and volatile? Explain your answer.
(b) Can a pointer be volatile? Explain your answer.
(c) What is wrong with the following function?:
```c
int square(volatile int ∗ptr)
{
  return ∗ptr ∗ ∗ptr;
}
```
# Bit Manipulation
## Question 9:
Embedded systems always require the user to manipulate bits in registers or
variables. Given an integer variable a, write two code fragments. The rst should
set bit 3 of a. The second should clear bit 3 of a. In both cases, the remaining
bits should be unmodified.

# Accessing fixed memory locations
## Question 10:
Embedded systems are often characterized by requiring the programmer to
access a specic memory location. On a certain project it is required to set
an integer variable at the absolute address 0x67a9 to the value 0xaa55. The
compiler is a pure ANSI compiler. Write code to accomplish this task.

# Interrupts
## Question 11:
Interrupts are an important part of embedded systems. Consequently, many
compiler vendors offer an extension to standard C to support interrupts. Typically,
this new key word is __interrupt. The following code uses __interrupt to dene
an interrupt service routine. Comment on the code.
```c
__interrupt double compute_area ( double r a d i u s )
{
double area = PI ∗ radius ∗ radius;
printf(' '\nArea = %f ' ', area);
return area;
}
```

# Code Ex
## Q12:
What does the following code output and why?
```
void foo(void)
{
  unsigned int a = 6;
  int b = −20;
  (a + b > 6) ? puts(">6") : puts("<=6");
}
```

## Q13:
Comment on the following code fragment?
```C
unsigned int zero = 0;
unsigned int compzero = 0xFFFF ; /∗ 1's complement of zero ∗/
```
-------------------------------------------------------------------------------

# Bonus - Dynamic memory allocation

## Q14:
Although not as common as in non-embedded computers, embedded systems
still do dynamically allocate memory from the heap. What are the problems
with dynamic memory allocation in embedded system.

# Typedef
## Q15:
Typedef is frequently used in C to declare synonyms for pre-existing data types.
It is also possible to use the preprocessor to do something similar. For instance,
consider the following code fragment:
```C
#define dPS struct s ∗
typedef struct s ∗ tPS ;
```
The intent in both cases is to dene dPS and tPS to be pointers to structure s.
Which method (if any) is preferred and why?

# Obfuscated syntax
## Q16:
C allows some appalling constructs. Is this construct legal, and if so what does
this code do?
```c
int a = 5, b = 7, c;
c = a +++ b;
```

===================================================================================

# Answers

## Q1
```c
#define SECONDS_PER_YEAR ( 60UL ∗ 60UL ∗ 24UL ∗ 365UL)
```
I'm looking for several things here:  
(a) Basic knowledge of the #dene syntax (i.e. no semi-colon at the end, the need to parenthesize etc.).  
(b) A good choice of name, with capitalization and underscores.   
(c) An understanding that the pre-processor will evaluate constant expressions for you.  
Thus, it is clearer, and penalty free to spell out how you are calculating the number of seconds in a year,  
rather than actually doing the calculation yourself.   
(d) A realization that the expression will overflow an integer argument on a 16 bit machine hence the need  
for the L, telling the compiler to treat the expression as a Long.  

## Q2


## Q3
The `#error` preprocessor directive in C and C++ is used to generate a compilation error with a custom error message.  
It is often used to enforce certain conditions or constraints at compile time.  
When the preprocessor encounters `#error`, it immediately halts the compilation process and outputs the specified error message along with the file name and line number where the `#error` directive was encountered.

Here's a basic example of how `#error` can be used:

```c
#include <stdio.h>

// Ensure that the architecture is supported
#if !defined(__x86_64__) && !defined(__i386__)
    #error "Unsupported architecture: Only x86_64 and i386 architectures are supported."
#endif

int main() {
    printf("Hello, world!\n");
    return 0;
}
```

In this example, if the code is compiled on an architecture other than x86_64 or i386, the compilation will fail with the specified error message. This can be useful for ensuring that code is only compiled on supported platforms or meets certain requirements before compilation proceeds.

Links: 
[](https://rmbconsulting.us/Publications/ErrorDirective.pdf)  
[](https://rmbconsulting.us/Publications/Efficient%20C%20Code.pdf)
