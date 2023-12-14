__Program Control__

_chtp9e ch4_


Iteration control
---
- by loop-continuation condition with a _control variable_ 
  - $⏰ ⋈ Threshold$, counter-controlled iteration
  - $🛂 ⋈ 🚦$, sentinel-controlled iteration
  - ⋈ is a relational operator
- iteration can be interrupted by
  - _continue_ or _break_


Counter-Controlled Iteration
---
```c
#include <stdio.h>

int main(void) {
   int counter = 1; // ❶ initialize

   while (counter <= 5) { // ❷ condition
      printf("%d  ", counter);
      ++counter; // ❸ update
   }

   puts("Done!");
}
```
- use integer counters
- don't use floating-point values which may be approximate


for Iteration Statement
---
```c
#include <stdio.h>
int main(void) {
   for (int counter = 1; // ❶ initialize
   counter <= 5; // ❷ condition
   ++counter) // ❸ update
   {
      printf("%d  ", counter);
   }

   puts("Done!"); 
}
```

📝 Practice
---
- draw the flowchart of the code above


Errors and special cases of iteration
---
- control variables (CVs) defined in a for header exist only until the loop terminates
  - accessing the CVs is a compilation error
- a logic error called an _off-by-one_ error: counter<5
- Infinite loops occur when the loop-continuation condition never becomes false
- Expressions in the for statement’s header are optional
   ```c
   // two infinite loops
   for(;;){;}

   while(true){;}
   ```
- Increment expression acts like a standalone statement


❓Questions
---
- Find the output of each for statement

```c
for (int i = 1; i <= 100; ++i) printf("%d\n", i);
for (int i = 100; i >= 1; --i) printf("%d\n", i);
for (int i = 7; i <= 77; i += 7) printf("%d\n", i);
for (int i = 20; i >= 2; i -= 2) printf("%d\n", i);
for (int j = 2; j <= 17; j += 3) printf("%d\n", i);
for (int j = 44; j >= 0; j -= 11) printf("%d\n", i);
```


Applications of the for statement
---
- Summing the even integers from 2 to 100
  - $\displaystyle S=∑_{n=2, n|2}^{100}n$
  ```c
  #include <stdio.h>

  int main(void)
  {
  int sum = 0;

  for (int number = 2; number <= 100; number += 2)
  {
      sum += number;
  }

  printf("Sum is %d\n", sum);
  }
  ```

- Compound-Interest Calculations
  - $a=p(1+r)^y$
  - Raise to power: [double pow (double base, double exponent)](https://cplusplus.com/reference/cmath/pow/)
  - [format string field width and alignment](https://cplusplus.com/reference/cstdio/printf/)
  ```c
  #include <stdio.h>
  #include <math.h>

  int main(void)
  {
    double principal = 1000.0;
    double rate = 0.05;

    printf("%4s%21s\n", "Year", "Amount on deposit");

    for (int year = 1; year <= 10; ++year)
    {

        double amount = principal * pow(1.0 + rate, year);
        // Formatting Numeric Output with field width
        printf("%4d%21.2f\n", year, amount);
    }
  }  
  ``` 

⚠️ Problems with floating numbers
---
```c
#include <stdio.h>
#include <math.h>

int main(void)
{
   // ❶ Displaying rounded values such as money
   // error accumulation and propagation
   double m1 = 15.323, m2 = 20.685; // internal values
   printf("m1=%.2f\nm2=%.2f\n", m1, m2); // rounded values
   printf("m1+m2=%.2f\n", m1+m2);

   // ❷ common dollar amounts can have
   // floating-point representational errors
   double d1 = 100.12, d2 = 99.01, d3 = 88.03;
   printf("d1 = %.15f\nd2 = %.15f\nd3 = %.15f\n", d1, d2, d3);
}
```


switch Multiple-Selection Statement
---
- counting letter grades
  - read character input with [int getchar ( void )](https://cplusplus.com/reference/cstdio/getchar/)
    - it returns the numerical representation of the character 
- EOF, end-of-file, normally equals -1, can be entered by
  - Ctrl+d, on Linux/MacOS
  - Ctrl+z, on Windows
```c
#include <stdio.h>

int main(void)
{
  int aCount = 0;
  int bCount = 0;
  int cCount = 0;
  int dCount = 0;
  int fCount = 0;

  puts("Enter the letter grades.");
  puts("Enter the EOF character to end input.");
  int grade = 0;
  // Read character input
  // Assignments have values
  while ((grade = getchar()) != EOF)
  {
    // show the input character
    printf("%c has the value %d.\n", grade, grade);
    switch (grade)
    {
    case 'A':
    case 'a':
        ++aCount;
        break;
    case 'B':
    case 'b':
        ++bCount;
        break;
    case 'C':
    case 'c':
        ++cCount;
        break;
    case 'D':
    case 'd':
        ++dCount;
        break;
    case 'F':
    case 'f':
        ++fCount;
        break;
    case '\n':
    case '\t':
    case ' ':
        break;
    default:
        printf("%s", "Incorrect letter grade entered.");
        puts(" Enter a new grade.");
        break;
    }
  }

  puts("\nTotals for each letter grade are:");
  printf("A: %d\n", aCount);
  printf("B: %d\n", bCount);
  printf("C: %d\n", cCount);
  printf("D: %d\n", dCount);
  printf("F: %d\n", fCount);
}
```


❓Questions
---
- How is the following expression evaluated?
  ```c
  a = b = c = 10;
  ```
  - = is right associate, evaluated from right to left
  - returns the value of the lhs


📝 Practice
---
-  ASCII (American Standard Code for Information Interchange) defines a character set and its numeric values 
   - it is a subset of Unicode


🔭 Explore
---
- [Comma operator](https://en.wikipedia.org/wiki/Comma_operator)