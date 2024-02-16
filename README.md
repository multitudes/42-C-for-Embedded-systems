# 42-C-for-Embedded-systems

10 Best Questions for Would-be Embedded Programmers.  
Very entertaining to read and study outside of a interview environment.

# Preprocessor Questions

## Question 1
Using the #define statement, how would you declare a manifest constant that
returns the number of seconds in a year? Disregard leap years in your answer.  

## Question 2
Write the standard MIN macro. That is, a macro that takes two arguments
and returns the smaller of the two arguments.  

## Question 3
What is the purpose of the preprocessor directive #error?

# Infinite loops

## Question 4
Innite loops often arise in embedded systems. How does one code an innite
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
What do the following incomplete2 declarations mean? 
```C
const int a ;
int const a ;
const int ∗a ;
int ∗ const a ;
int const ∗ a const;
```

## Question 8
What does the keyword volatile mean? Give three different examples of its use.

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

# Accessing fixed memory locations
## Question 10:
Embedded systems are often characterized by requiring the programmer to
access a specic memory location. On a certain project it is required to set
an integer variable at the absolute address 0x67a9 to the value 0xaa55. The
compiler is a pure ANSI compiler. Write code to accomplish this task.

# Interrupts
## Question 11:
Interrupts are an important part of embedded systems. Consequently, many
compiler vendors oer an extension to standard C to support interrupts. Typically,
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
int a = 5, b = 7, c;
c = a +++ b;

Links: 
[](https://rmbconsulting.us/Publications/ErrorDirective.pdf)  
[](https://rmbconsulting.us/Publications/Efficient%20C%20Code.pdf)
