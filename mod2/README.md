__Formatted Input/Output__

_chtp9e ch9_


Streams
---
- Interacting with users is the interface of programs
  - performed with sequences of bytes called _streams_
- Three standard streams
  - `stdin` connected to the keyboard for input
  - `stdout` connected to the screen for output
  - `stderr` connected to the screen for showing errors
  - these streams can be redirected to other devices
- Two representative functions
  - `printf`: formatted output
  - `scanf`: formatted input
  - input/output functions are colleted in `stdio.h`


Formatting Output with printf
---
- syntax: `printf(format-control-string, data-list)`
  - format data-list according to the format-control-string
- format control string: 
  - `%[flags][width][.precision][length]specifier`


Printing integers
---
```c
#include <stdio.h>

int main(void) {
   printf("%d\n", 521);
   printf("%i\n", 521); 
   printf("%d\n", +521); 
   printf("%d\n", -521); 
   printf("%hd\n", 1314); 
   printf("%ld\n", 52113141314L); 
   printf("%o\n", 521); 
   printf("%u\n", 521);
   printf("%u\n", -521); // ⚠️ two's complement
   printf("%x\n", 521); 
   printf("%X\n", 521); 
} 
```

Integer format specifier and length
---
| output format | specifier |
| --- | --- |
| Signed decimal integer | d  i |
| Unsigned decimal integer | u |
| Unsigned octal | o |
| Unsigned lowercase hexadecimal integer | x |
| Unsigned uppercase hexadecimal integer | X |

| length\specifier | d i | u o x X |
| --- | --- | --- |
|  | int | unsigned int |
| hh | signed char | unsigned char |
| h	| short int | unsigned short int |
| l	| long int |	unsigned long int |
| ll | long long int | unsigned long long int |


Printing Floating-Point Numbers
---
```c
#include <stdio.h>

int main(void) {
  printf("%e\n", 52113.14);
  printf("%e\n", +52113.14); 
  printf("%e\n", -52113.14); 
  printf("%E\n", 52113.14);
  printf("%f\n", 52113.14);
  printf("%F\n", 52113.14);
  printf("%g\n", 52113.14); 
  printf("%G\n", 52113.14); 

  printf("%e\n", -13.14); 
  printf("%E\n", 13.14);
  printf("%f\n", 13.14);
  printf("%F\n", 13.14);
  printf("%g\n", 13.14); 
  printf("%G\n", 13.14);    
} 
```

Floating-point format specifier and length
---
| output format | specifier |
| --- | --- |
| Decimal floating point, lowercase | f |
| Decimal floating point, uppercase | F |
| Scientific notation (mantissa/exponent), lowercase | e |
| Scientific notation (mantissa/exponent), uppercase | E |
| Use the shortest representation: %e or %f | g |
| Use the shortest representation: %E or %F | G |
| Hexadecimal floating point, lowercase | a |
| Hexadecimal floating point, uppercase | A |

| length\specifier | 	f F e E g G a A	 |
| --- | --- | 
|  | double |
| L	| long double |


Printing Strings and Characters
---
```c
#include <stdio.h>

int main(void) {
  char character = 'A'; 
  printf("%c\n", character);

  printf("%s\n", "Errors should never pass silently.");

  char string[] = "Readability counts."; 
  printf("%s\n", string);

  const char *stringPtr = "Flat is better than nested."; 
  printf("%s\n", stringPtr);

  printf("%s\n", character); // ⚠️❶ 
  printf("%c\n", string); // ⚠️❷
} 
```
- ❶ Using %c to print a string is a _logic error_
- ❷ Using %s to print a char argument usually causes 
  - a fatal runtime logic error called an _access violation_
  - `Segmentation fault` on Linux


Format width, precision, alignment and padding
---
- format control string: 
  - `%[flags][width][.precision][length]specifier`

```c
#include <stdio.h>

int main(void) {
  puts("❶ Field widths for integers>");
  printf("%4d\n", 1);
  printf("%4d\n", 12);
  printf("%4d\n", 123);
  printf("%4d\n", 1234);
  printf("%4d\n\n", 12345);

  printf("%4d\n", -1);
  printf("%4d\n", -12);
  printf("%4d\n", -123);
  printf("%4d\n", -1234);
  printf("%4d\n", -12345);
  puts("\n\n");

  puts("❷ Precisions for integers, floating-point numbers and strings");
  puts("➀ Using precision for integers");
  int i = 1314; 
  printf("\t%.2d\n\t%.4d\n\t%.7d\n\t%.9d\n\n", i, i, i, i);

  puts("➁ Using precision for floating-point numbers");
  double f = 521.131415; 
  printf("\t%.2f\n\t%.3f\n\t%.3e\n\t%.3g\n\n", f, f, f, f);
  
  puts("➂ Using precision for strings");
  char s[] = "Happy New Year"; 
  printf("\t%.8s\n\t%.11s\n\t%.20s\n", s, s, s); 

  puts("❸ Combine field widths and precisions");
  printf("%5.3f\n%10.4f\n%15.5f\n%20.10f\n", f, f, f, f);

  puts("❹ Specify field widths and precisions dynamically");
  printf("%*.*f\n", 5, 3, f);
  printf("%*.*f\n", 10, 4, f);
  printf("%*.*f\n", 15, 5, f);
  printf("%*.*f\n", 20, 10, f);     
} 
```
- ❶ Field width for integer
  - #integer digits ≤ field width: right aligned
    - left padded with spaces
  - #integer digits > field width: all digits displayed
    - alignment corrupted
- ❷ Precision
  - ➀ for integer specifier: indicates the minimum #digits to be printed
    - if #digits < precision
      - left padded with 0s if precision prefixed with . or 0
      - left padded with spaces if only precision
    - the default precision is 1 for integers
  - ➁ for floating-point specifier 
    - e,E,f,F: indicates #digits after the decimal point
    - g,G: indicates the maximum number of significant digits
  - ➂ for string specifier s
    - indicates the maximum number of characters from the beginning of the string


printf Format Flags
---
```c
#include <stdio.h>

int main(void) {
  puts("❶ Right- and left-aligning values");
  puts("1234567890123456789012345678901234567890");
  printf("%10s%10d%10c%10f\n\n", "hello", 7, 'a', 1.23);
  puts("1234567890123456789012345678901234567890");
  printf("%-10s%-10d%-10c%-10f\n", "hello", 7, 'a', 1.23);

  puts("❷ Printing positive and negative numbers with and without the + flag");
  printf("%d\n%d\n", 786, -786);
  printf("%+d\n%+d\n", 786, -786); 

  puts("❸ Using the space flag not preceded by + or -");
  printf("% d\n% d\n", 547, -547);

  puts("❹ Using the # flag with conversion specifiers\n"
  "o, x, X and any floating-point specifier");
  int c = 521; 
  printf("%#o\n", c);
  printf("%#x\n", c);
  printf("%#X\n", c);
  
  double p = 13.14; 
  printf("\n%g\n", p);
  printf("%#g\n", p); 

  puts("❺ Using the 0 (zero) flag");
  printf("%+09d\n", 521);
  printf("%09d\n", 521);     
} 
```

| Flag | Description |
| --- | --- |
| `-` | ❶ Left-align the output within the specified field |
| `+` | ❷ Display a plus sign preceding a positive value and  a minus sign preceding a negative value |
| `␣` | ❸ Print a space before a positive value not printed with the + flag |
| `#` | ❹ ▶️prefix the output with 0 for specifier o<br/>▶️prefix the output with 0x or 0X for specifier x or X respectively<br/>▶️Force a decimal point for a floating-point number without a fractional part printed with e, E, f, g or G. For g and G specifiers, trailing zeros are not eliminated. Normally, the decimal point is printed only if a digit follows it |
| `0` | ❺ Pad a field with leading zeros |


Printing Literals and Escape Sequences
---
```c
#include <stdio.h>

int main(void) {
   printf("\'\"\?\\\n");
   printf("\a\n");
   printf("hell\bo\f");
   printf("hell\roc\n");
   printf("hell\to\n");
   printf("hell\vo\n");
} 
```
- escape sequence = `\` followed by an escape character
  - describes control characters

| Escape sequence | Description |
| --- | --- |
| `\'` | single quote |
| `\"` | double quote |
| `\?` | question mark |
| `\\` | backslash |
| `\a` | alert or bell, causes an audible (bell) or visual alert |
| `\b` | backspace, moves the cursor back one position on the current line |
| `\f` | new page or form feed , moves the cursor to the next logical page’s start|
| `\n` | newline, moves the cursor to the beginning of the next line |
| `\r` | carriage return, moves the cursor to the beginning of the current line |
| `\t` | horizontal tab, moves the cursor to the next horizontal tab position |
| `\v` | vertical tab, moves the cursor to the next vertical tab position |


🔭 Explore
---
- [Print formatted data to stdout](https://cplusplus.com/reference/cstdio/printf/)
  - [Formatted input/output](https://en.cppreference.com/w/c/io)
- [ASCII chart](https://en.cppreference.com/w/c/language/ascii)
  - [Character sets and encodings](https://en.cppreference.com/w/c/language/charset)
    - [Character constant](https://en.cppreference.com/w/c/language/character_constant)
  - [Escape sequences](https://en.cppreference.com/w/c/language/escape)


Formatted Input with `scanf`
---
- `scanf` syntax:
  - `scanf(format-control-string, input-holding-pointers);`
  - format-control-string
    - `%[*][width][length]specifier` 
    - indicates the format of the data to be input
- `scanf` can 
  - input all types of data
  - input specific characters from an input stream
  - skip specific characters in the input stream

```c
#include <stdio.h>

int main(void) {
   puts("❶ Reading Integers");
   int a,b,c,d,e,f,g; 
   puts("Enter seven integers: ");
   scanf("%d%i%i%i%o%u%x", &a, &b, &c, &d, &e, &f, &g);
   puts("\nThe input displayed as decimal integers is:");
   printf("%d %d %d %d %d %d %d\n\n", a, b, c, d, e, f, g);

   puts("❷ Reading Floating-Point Numbers");
   double d1, d2, d3;
   puts("Enter three floating-point numbers:");
   scanf("%le%lf%lg", &d1, &d2, &d3);
   puts("\nUser input displayed in plain floating-point notation:");
   printf("%f\n%f\n%f\n", d1, d2, d3);

   puts("❸ Reading Characters and Strings");
   char ch = '\0'; 
   char str[9] = "";    
   printf("%s", "Enter a string: ");
   scanf("%c%8s", &ch, str);
   printf("The input was '%c' and \"%s\"\n", ch, str);   

   puts("❹ Using Scan Sets");
   char z[9] = "";    
   printf("%s", "Enter string: ");
   scanf("%8[aeiou]", z); // stop at the first character NOT in the set
   printf("The input was \"%s\"\n", z);

   puts("❺ Using an inverted scan set");
   char zi[9] = "";
   printf("%s", "Enter a string: ");
   scanf("%8[^aeiou]", zi); // stop at the first character in the set
   printf("The input was \"%s\"\n", zi);

   puts("❻ Using field width");
   int w1, w2;   
   printf("%s", "Enter a six digit integer: ");
   scanf("%2d%d", &w1, &w2);
   printf("The integers input were %d and %d\n", w1, w2);   

   puts("❼ Skipping Characters in an Input Stream");
   int month, day, year;  
   printf("%s", "Enter a date in the form mm-dd-yyyy: ");
   scanf("%d%*c%d%*c%d", &month, &day, &year);
   printf("month = %d  day = %d  year = %d\n\n", month, day, year);   
   printf("%s", "Enter a date in the form mm/dd/yyyy: ");
   scanf("%d%*c%d%*c%d", &month, &day, &year);
   printf("month = %d  day = %d  year = %d\n", month, day, year);      
} 
```


scanf Conversion Specifiers
---
| Specifier | Expected input | argument type |
| --- | --- | --- |
| __Integers__ | | |
| d | an optionally signed decimal integer | int*  |
| i | an optionally signed decimal, octal or hexadecimal integer | int*  |
| o | an octal integer | unsigned int*  |
| u | an unsigned decimal integer | unsigned int*  |
| x X | a hexadecimal integer | unsigned int*  |
| h l ll | Place before any integer conversion specifier to indicate the integer length | short*,long* or long long*  |
| __Floating-point numbers__ | | |
| e E f g  G | a floating-point value |  float* or double*  |
| l L | Place before any floating-point conversion specifier to indicate the floating-point length | double* or long double* |
| __Characters and strings__ | | |
| c | a character | char* |
| s | a string |  an array of type char that’s large enough to hold the string and a automatically-added `\0` |
| __Scan set__ | | |
| [scan characters] | Scan a string for a set of characters that are stored in an array, stop at the first character not in the set |  |
| __Miscellaneous__ | | |
| P | an address of the same form produced when an address is output with %p in a printf statement | void** |
| n | Returns the number of characters read so far. No input is consumed. |  |
| % | Skip a `%` in the input |  |

- assignment suppression character `*`
  - enables scanf to read and discard data from the input without assigning it to a variable. e.g. 
  - `%*c` read and discard one character
  - `%*d` read and discard a decimal integer


🔭 Explore
---
- [scanf - Read formatted data from stdin](https://cplusplus.com/reference/cstdio/scanf/)
  - [scanf, fscanf, sscanf, scanf_s, fscanf_s, sscanf_s](https://en.cppreference.com/w/c/io/fscanf)