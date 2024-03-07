# 42-C-for-Embedded-systems

> C is quirky, flawed, and an enormous success. — Dennis Ritchie

10 Best Questions for Would-be Embedded Programmers.  
(Very entertaining to read and study outside of a interview environment.)

# Preprocessor Questions

## Question 1
Using the `#define` statement, how would you declare a manifest constant that
returns the number of seconds in a year?  
Disregard leap years in your answer.  

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
(e) As a bonus, if you modied the expression with a UL (indicating unsigned long),  
then you are o to a great start because you are showing that you are mindful of the perils of signed  
and unsigned types  and remember, first impressions count!  

## Q2
```c
#define MIN(A, B) ( (A) <= (B) ? (A) : (B) )
```
The purpose of this question is to test the following:  
(a) Basic knowledge of the #define directive as used in macros.  
This is important, because until the inline operator becomes part of standard C,  
macros are the only portable way of generating inline code. Inline code is often necessary in embedded systems in
order to achieve the required performance level.
(b) Knowledge of the ternary conditional operator. This exists in C because
it allows the compiler to potentially produce more optimal code than an if-
then-else sequence. Given that performance is normally an issue in embedded
systems, knowledge and use of this construct is important.
(c) Understanding of the need to very carefully parenthesize arguments to
macros.
(d) I also use this question to start a discussion on the side eects of macros,
e.g. what happens when you write code such as :
l e a s t = MIN( ∗ p++, b ) ;

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

## Q4
There are several solutions to this question. My preferred solution is:
```c
while ( 1 )
{
...
}
```
Another common construct is:
```c
for ( ; ; )
{
...
}
```
Personally, I dislike this construct because the syntax doesn't exactly spell out
what is going on. Thus, if a candidate gives this as a solution, I'll use it as an
opportunity to explore their rationale for doing so. If their answer is basically  
I was taught to do it this way and I have never thought about it since then
it tells me something (bad) about them. Conversely, if they state that it's the
K&R preferred method and the only way to get an infinite loop passed Lint, then they 
score bonus points. A third solution is to use a goto:  
Loop :
```c
...
goto Loop ;
```
Candidates that propose this are either assembly language programmers (which
is probably good), or else they are closet BASIC / FORTRAN programmers
looking to get into a new field.

## Q5

The answers are:
```
int a; // An integer
int *a; // A pointer to an integer
int **a; // A pointer to a pointer to an integer
int a[10]; // An array of 10 integers
int *a[10]; // An array of 10 pointers to integers
int (*a)[10]; // A pointer to an array of 10 integer
int (*a)(int); // A pointer to a function a that takes an integer argument and returns an integer
int (*a[10])(int); // An array of 10 pointers to functions that takes an integer argument and returns an integer
```


----------------------------------------------------
## Static 

People often claim that a couple of these are the sorts of thing that one looks
up in textbooks  and I agree. While writing this article, I consulted textbooks
to ensure the syntax was correct. However, I expect to be asked this question
(or something close to it) when in an interview situation. Consequently, I make
sure I know the answers  at least for the few hours of the interview. Candidates
that don't know the answers (or at least most of them) are simply unprepared
for the interview. If they can't be prepared for the interview, what will they be
prepared for?

## Q6
What are the uses of the keyword static?
This simple question is rarely answered completely. Static has three distinct
uses in C:
(a) A variable declared static within the body of a function maintains its value
between function invocations.
(b) A variable declared static within a module1 , (but outside the body of
a function) is accessible by all functions within that module. It is not
accessible by functions within any other module. That is, it is a localized
global.
(c) Functions declared static within a module may only be called by other
functions within that module. That is, the scope of the function is localized
to the module within which it is declared.
Most candidates get the rst part correct. A reasonable number get the second
part correct, while a pitiful number understand answer (c). This is a serious
weakness in a candidate, since they obviously do not understand the importance
and benets of localizing the scope of both data and code.

## Const

## Q7
As soon as the interviewee says const means constant, I know I'm dealing
with an amateur. Dan Saks has exhaustively covered const in the last year,
such that every reader of ESP should be extremely familiar with what const
can and cannot do for you. If you haven't been reading that column, suce
it to say that const means read-only. Although this answer doesn't really do
the subject justice, I'd accept it as a correct answer. (If you want the detailed
answer, then read Saks' columns  carefully!).
If the candidate gets the answer correct, then I'll ask him these supplemental
questions:
What do the following incomplete2 declarations mean?
const int a ;
int const a ;
const int ∗ a ;
int ∗ const a ;
int const ∗ a const

The rst two mean the same thing, namely a is a const (read-only) integer. The
third means a is a pointer to a const integer (i.e., the integer isn't modiable,
but the pointer is). The fourth declares a to be a const pointer to an integer
(i.e., the integer pointed to by a is modiable, but the pointer is not). The nal
declaration declares a to be a const pointer to a const integer (i.e., neither the
integer pointed to by a, nor the pointer itself may be modied).
If the candidate correctly answers these questions, I'll be impressed.
Incidentally, one might wonder why I put so much emphasis on const, since it is
very easy to write a correctly functioning program without ever using it. There
are several reasons:
(a) The use of const conveys some very useful information to someone reading
your code. In eect, declaring a parameter const tells the user about its
intended usage. If you spend a lot of time cleaning up the mess left by
other people, then you'll quickly learn to appreciate this extra piece of
information. (Of course, programmers that use const, rarely leave a mess
for others to clean up...)
(b) const has the potential for generating tighter code by giving the optimizer
some additional information.
(c) Code that uses const liberally is inherently protected by the compiler
against inadvertent coding constructs that result in parameters being
changed that should not be. In short, they tend to have fewer bugs.

## Volatile

## A8
A volatile variable is one that can change unexpectedly. Consequently, the
compiler can make no assumptions about the value of the variable. In particular,
the optimizer must be careful to reload the variable every time it is used instead
of holding a copy in a register. Examples of volatile variables are:
(a) Hardware registers in peripherals (e.g., status registers)
(b) Non-stack variables referenced within an interrupt service routine.
(c) Variables shared by multiple tasks in a multi-threaded application.
If a candidate does not know the answer to this question, they aren't hired. I
consider this the most fundamental question that distinguishes between a `C
programmer' and an `embedded systems programmer'. Embedded folks deal
with hardware, interrupts, RTOSes, and the like. All of these require volatile
variables. Failure to understand the concept of volatile will lead to disaster. On
the (dubious) assumption that the interviewee gets this question correct, I like
to probe a little deeper, to see if they really understand the full signicance of
volatile. In particular, I'll ask them the following:
Q8.1:
(a) Can a parameter be both const and volatile? Explain your answer.
(b) Can a pointer be volatile? Explain your answer.
(c) What is wrong with the following function?:
```
int square(volatile int ∗ptr)
{
  return (∗ptr ∗ ∗ptr);
}
```
The answers are as follows:
(a) Yes. An example is a read only status register. It is volatile because it can
change unexpectedly. It is const because the program should not attempt
to modify it.
(b) Yes. Although this is not very common. An example is when an interrupt
service routine modies a pointer to a buer.
(c) This one is wicked. The intent of the code is to return the square of
the value pointed to by *ptr. However, since *ptr points to a volatile
parameter, the compiler will generate code that looks something like this:
```
int square(volatile int ∗ptr)
{
  a = ∗ptr;
  b = ∗ptr;
  return a ∗ b;
}
```
Since it is possible for the value of *ptr to change unexpectedly, it is possible
for a and b to be dierent. Consequently, this code could return a number that
is not a square! The correct way to code this is:
```
long square(volatile int ∗ptr)
{
  int a;
  a = ∗ptr;
  return a ∗ a;
}
```



Links: 
[](https://rmbconsulting.us/Publications/ErrorDirective.pdf)  
[](https://rmbconsulting.us/Publications/Efficient%20C%20Code.pdf)
