__Introduction to C Programming Language__

💡 Demo: Print text
---
```c
/* hello.c
print greetings
*/

// function main begins program execution
int main(void){
  printf("Welcome to C!\n"); // ; ends a statement
}
```
- explain the following concepts
  - C program structure
    - header files
    - libraries
      - output statements with [_printf_](https://cplusplus.com/reference/cstdio/printf/)
        - use [_puts_](https://en.cppreference.com/w/cpp/io/c/puts) function to display a string
      - escape sequences: new line (\\n), tab (\\t), alert (\\a), backslash (\\), quote (\\")
    - main function
    - block
  - comments: single line comment, multi-line comments
  - preprocessor directives
  - bland lines and white spaces
  - indentation conventions
  - case sensitivity


📝 Practice
---
- print multiple lines
  - with multiple printf
  - with a single printf
- print [ascii art](https://www.asciiart.eu/)


💡Demo: Arithmetic in C
---
- Add two integers

```c
#include <stdio.h>

int main(void) {
   int integer1 = 0, integer2 = 0;
   int sum = 0; 

   printf("Enter first integer: ");
   scanf("%d", &integer1);

   printf("Enter second integer: "); 
   scanf("%d", &integer2);

   sum = integer1 + integer2; 
   printf("%d + %d = %d\n", integer1, integer2, sum); 
}
```
- Explain the following concepts
  - variables and their definitions
    - type and initialization
    - define before they are used
    - identifiers
      - camel casing
  - prompting messages
  - the [_scanf_](https://cplusplus.com/reference/cstdio/scanf/) function and formatted input
    - format control string
    - conversion specification
    - address operator
  - assignment statement
  - binary operators
  - print with a format control string
  - combine variable definition and assignment
  - calculations in printf statements


💡 Demo: memory concepts
---
- show variables in memory
  - placing a value into a memory is destructive
  - read the value from a memory is non-destructive


💡 Demo: [arithmetic operators](https://en.cppreference.com/w/c/language/operator_arithmetic)
---
- integer division and the remainder operator
- arithmetic expressions in straight-line form
- parentheses for grouping sub-expressions
- [rules of operator precedence](https://en.cppreference.com/w/c/language/operator_precedence)
- operator's grouping or associativity


📝 Practice
---
- Write the straight-line form in C for the following math formula
  - $\displaystyle m=\frac{a+b+c+d+e}{5}$
  - $\displaystyle a+b+c+d+\frac{e}{5}$
  - $\displaystyle z=pr\mod q + w/x -y$
- Parentheses on the same level are evaluated left-to-right
  - $\displaystyle a×(b+c)+c×(d+e)$
- Evaluate a second-degree polynomial (quadratic polynomial)
  - $\displaystyle y=ax^2 + bx +c$
  - use parentheses for clarity


💡 Demo: compare numbers
---
```c
#include <stdio.h>

int main(void) {
   printf("Enter two integers, and I will tell you\n"
          "the relationships they satisfy: ");

   int number1 = 0; 
   int number2 = 0; 
   
   scanf("%d %d", &number1, &number2); 
   
   if (number1 == number2) {                          
      printf("%d is equal to %d\n", number1, number2);
   } 

   if (number1 != number2) {
      printf("%d is not equal to %d\n", number1, number2);
   } 

   if (number1 < number2) {
      printf("%d is less than %d\n", number1, number2);
   } 

   if (number1 > number2) {
      printf("%d is greater than %d\n", number1, number2);
   } 

   if (number1 <= number2) {
      printf("%d is less than or equal to %d\n", number1, number2);
   } 

   if (number1 >= number2) {
      printf("%d is greater than or equal to %d\n", number1, number2);
   } 
} 
```
- explain the following concepts
  - make decision based on condition
    - a condition is a boolean expression can be true or false
  - if statement
  - [equality and relational operators](https://en.cppreference.com/w/c/language/operator_comparison)
  - [logical operators](https://en.cppreference.com/w/c/language/operator_logical)
  - equality operator vs assignment operator