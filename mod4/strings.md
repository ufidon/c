__Characters and Strings__

_chtp9e ch8_

Functions manipulating characters and strings
---
| functions | library |
| --- | --- |
| handle characters | `ctype.h` |
| string conversion and general utilities | `stdlib.h` |
| input/output for strings and characters | `stdio.h` |
| string and memory processing | `string.h` |


Characters and strings
---
- A character constant or literal is an _int value_ represented as _a character in single quotes_
  - e.g. `'x', '8', '#'`
- A string literal or constants is a _group of characters in double quotes_ 
  - strings are null (`\0`) terminated
  - the string name is a `const char *` pointer 
    - pointed to the first character of the string


Initialize char array and char * pointers
---
```c
char name[] = "Donald Trump";
const char *organization = "White house";
char title[] = {'U', 'S', 'A', ' ', 'P', 'r', 'e', 's', 'i', 'd', 'e', 'n', 't', '\0'};
```

Read string and character
---
```c
char name[20];
scanf("%19s", name);

char ch;
scanf("%c", &ch);
```

Handle characters
---
- determine character type
```c
#include <ctype.h>
#include <stdio.h>

int main(void)
{
  printf("%s\n%s%s\n%s%s\n\n", "According to isdigit: ",
        isdigit('8') ? "8 is a " : "8 is not a ", "digit",
        isdigit('#') ? "# is a " : "# is not a ", "digit");

  printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n", "According to isalpha:",
        isalpha('A') ? "A is a " : "A is not a ", "letter",
        isalpha('b') ? "b is a " : "b is not a ", "letter",
        isalpha('&') ? "& is a " : "& is not a ", "letter",
        isalpha('4') ? "4 is a " : "4 is not a ", "letter");

  printf("%s\n%s%s\n%s%s\n%s%s\n\n", "According to isalnum:",
        isalnum('A') ? "A is a " : "A is not a ", "digit or a letter",
        isalnum('8') ? "8 is a " : "8 is not a ", "digit or a letter",
        isalnum('#') ? "# is a " : "# is not a ", "digit or a letter");

  printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n%s%s\n", "According to isxdigit:",
        isxdigit('F') ? "F is a " : "F is not a ", "hexadecimal digit",
        isxdigit('J') ? "J is a " : "J is not a ", "hexadecimal digit",
        isxdigit('7') ? "7 is a " : "7 is not a ", "hexadecimal digit",
        isxdigit('$') ? "$ is a " : "$ is not a ", "hexadecimal digit",
        isxdigit('f') ? "f is a " : "f is not a ", "hexadecimal digit");
  printf("%s\n%s%s%s\n%s%s%s\n%s%s\n\n", "According to isspace:",
          "Newline", isspace('\n') ? " is a " : " is not a ",
          "whitespace character",
          "Horizontal tab", isspace('\t') ? " is a " : " is not a ",
          "whitespace character",
          isspace('%') ? "% is a " : "% is not a ", "whitespace character");

  printf("%s\n%s%s%s\n%s%s\n\n", "According to iscntrl:",
          "Newline", iscntrl('\n') ? " is a " : " is not a ",
          "control character",
          iscntrl('$') ? "$ is a " : "$ is not a ", "control character");

  printf("%s\n%s%s\n%s%s\n%s%s\n\n", "According to ispunct:",
          ispunct(';') ? "; is a " : "; is not a ", "punctuation character",
          ispunct('Y') ? "Y is a " : "Y is not a ", "punctuation character",
          ispunct('#') ? "# is a " : "# is not a ", "punctuation character");

  printf("%s\n%s%s\n%s%s%s\n\n", "According to isprint:",
          isprint('$') ? "$ is a " : "$ is not a ", "printing character",
          "Alert", isprint('\a') ? " is a " : " is not a ",
          "printing character");

  printf("%s\n%s%s\n%s%s%s\n", "According to isgraph:",
          isgraph('Q') ? "Q is a " : "Q is not a ",
          "printing character other than a space",
          "Space", isgraph(' ') ? " is a " : " is not a ",
          "printing character other than a space");        
}
```

- determine and convert letter case
```c
#include <ctype.h>
#include <stdio.h>

int main(void)
{
  printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n", "According to islower:",
        islower('p') ? "p is a " : "p is not a ", "lowercase letter",
        islower('P') ? "P is a " : "P is not a ", "lowercase letter",
        islower('5') ? "5 is a " : "5 is not a ", "lowercase letter",
        islower('!') ? "! is a " : "! is not a ", "lowercase letter");

  printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n", "According to isupper:",
        isupper('D') ? "D is an " : "D is not an ", "uppercase letter",
        isupper('d') ? "d is an " : "d is not an ", "uppercase letter",
        isupper('8') ? "8 is an " : "8 is not an ", "uppercase letter",
        isupper('$') ? "$ is an " : "$ is not an ", "uppercase letter");

  printf("%s%c\n%s%c\n%s%c\n%s%c\n",
        "u converted to uppercase is ", toupper('u'),
        "7 converted to uppercase is ", toupper('7'),
        "$ converted to uppercase is ", toupper('$'),
        "L converted to lowercase is ", tolower('L'));
}
```


🔭 Explore
---
- [Functions for character classification and manipulation](https://en.cppreference.com/w/c/string/byte)


Conversion between strings and numbers
---
```c
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

int main(void)
{
  put("❶ string to double");  
  const char *string1 = "51.2% are admitted";
  char *remainderPtr1 = NULL;

  double d = strtod(string1, &remainderPtr1);

  printf("The string \"%s\" is converted to the\n", string1);
  printf("double value %.2f and the remainder string \"%s\"\n", d, remainderPtr1);


  put("\n❷ string to long int");
  const char *string2 = "-1234567abc"; 
  char *remainderPtr2 = NULL;
  
  long x = strtol(string2, &remainderPtr2, 0);

  printf("%s\"%s\"\n%s%ld\n%s\"%s\"\n%s%ld\n",
    "The original string is ", string2,
    "The converted value is ", x,
    "The remainder of the original string is ", remainderPtr2,
    "The converted value plus 567 is ", x + 567);


  put("\n❸ string to unsigned long int");
  const char *string3 = "1234567abc"; 
  char *remainderPtr3 = NULL; 

  unsigned long int y = strtoul(string3, &remainderPtr3, 0);

  printf("%s\"%s\"\n%s%lu\n%s\"%s\"\n%s%lu\n",
    "The original string is ", string3,
    "The converted value is ", y,
    "The remainder of the original string is ", remainderPtr3, 
    "The converted value minus 567 is ", y - 567);
}
```


🔭 Explore
---
- [Functions for string conversions to and from numeric formats](https://en.cppreference.com/w/c/string/byte)


Character/string input/output
---
```c
#include <stdio.h>
#define SIZE 80

void reverse(const char *const);

int main(void)
{
  puts("❶ Stdin to string> Enter a line of text:");
  char sentence[SIZE] = "";
  fgets(sentence, SIZE, stdin);
  printf("\n%s", "The line printed backward is:");
  reverse(sentence); puts("");

  puts("❷ Stdin to character> Enter a line of text:");
  int c = 0;
  char sentence2[SIZE] = "";
  int i = 0;
  while ((i < SIZE - 1) && (c = getchar()) != '\n')
  {
    sentence2[i++] = c;
  }
  sentence2[i] = '\0';
  puts("\nThe line entered was:");
  puts(sentence2); puts("");

  puts("❸ Format string> Number to string:");
  int x = 0; 
  double y = 0.0; 
  puts("Enter an integer and a double:");
  scanf("%d%lf", &x, &y);
  char s[SIZE] = ""; // create char array
  sprintf(s, "integer:%6d\ndouble:%7.2f", x, y);  
  printf("The formatted output stored in array s is:\n%s\n\n", s); 

  puts("❹ Format input> String to number");
  char s2[] = "31298 87.375"; 
  int x2 = 0; 
  double y2 = 0; 
  sscanf(s2, "%d%lf", &x2, &y2); 
  puts("The values stored in character array s2 are:");
  printf("integer:%6d\ndouble:%8.3f\n", x2, y2);   
}

void reverse(const char *const sPtr)
{
  if ('\0' == sPtr[0])
  {
    return;
  }
  else
  {
    reverse(&sPtr[1]);
    putchar(sPtr[0]);
  }
}
```

🔭 Explore
---
- [Functions for string/character input/output](https://en.cppreference.com/w/c/io)


String manipulation
---
- copy and concatenate strings
- compare strings
- search strings for characters and sub strings
- tokenizing strings
- determine the length of strings


```c
#include <stdio.h>
#include <string.h>
#define SIZE1 25
#define SIZE2 15

int main(void) {
  puts("❶ copy strings:");
  char x[] = "12345678901234567890"; 
  char y[SIZE1] = ""; 
  char z[SIZE2] = ""; 

  printf("%s%s\n%s%s\n", 
    "The string in array x is: ", x,
    "The string in array y is: ", strcpy(y, x));

  strncpy(z, x, SIZE2 - 1); 
  z[SIZE2 - 1] = '\0'; 
  printf("The string in array z is: %s\n", z);
  puts("");

  puts("❷ concatenate strings:");
  char s1[20] = "Happy ";
  char s2[] = "New Year ";
  char s3[40] = "";
  printf("s1 = %s\ns2 = %s\n", s1, s2);
  printf("strcat(s1, s2) = %s\n", strcat(s1, s2));
  printf("strncat(s3, s1, 6) = %s\n", strncat(s3, s1, 6));
  printf("strcat(s3, s1) = %s\n\n", strcat(s3, s1));

  puts("❸ compare strings:");
   const char *str1 = "Happy New Year"; 
   const char *str2 = "Happy New Year"; 
   const char *str3 = "Happy Holidays"; 
 
  printf("str1 = %s\ns2 = %s\ns3 = %s\n\n%s%2d\n%s%2d\n%s%2d\n\n",
    str1, str2, str3,
    "strcmp(str1, str2) = ", strcmp(str1, str2),
    "strcmp(str1, str3) = ", strcmp(str1, str3),
    "strcmp(str3, str1) = ", strcmp(str3, str1));

  printf("%s%2d\n%s%2d\n%s%2d\n",
    "strncmp(str1, str3, 6) = ", strncmp(str1, str3, 6),
    "strncmp(str1, str3, 7) = ", strncmp(str1, str3, 7),
    "strncmp(str3, str1, 7) = ", strncmp(str3, str1, 7));
  puts("");

  puts("❹ search characters in strings:");
  const char *string = "This is a test";
  char character1 = 'a';
  char character2 = 'z';
  // ➀ strchr searches from left to right
  if (strchr(string, character1) != NULL)
    printf("\'%c\' was found in \"%s\".\n", character1, string);
  else
    printf("\'%c\' was not found in \"%s\".\n", character1, string);

  if (strchr(string, character2) != NULL)
    printf("\'%c\' was found in \"%s\".\n", character2, string);
  else
    printf("\'%c\' was not found in \"%s\".\n\n", character2, string); 
  // ➁ strrchr searches reversely, from right to left
  if (strrchr(string, character1) != NULL)
    printf("\'%c\' was found in \"%s\".\n", character1, string);
  else
    printf("\'%c\' was not found in \"%s\".\n", character1, string);

  if (strrchr(string, character2) != NULL)
    printf("\'%c\' was found in \"%s\".\n", character2, string);
  else
    printf("\'%c\' was not found in \"%s\".\n\n", character2, string);


  puts("❺ strcspn searches substring containing no specified characters:");
  const char *string1 = "The value is 3.14159";
  const char *charset1 = "1234567890";
  // ➀ strcspn determines the length of the initial part of its first 
  // argument that does NOT contain any characters from its second argument
  printf("string1 = %s\ncharset1 = %s\n\n%s\n%s%zu\n", string1, charset1,
    "The length of the initial segment of string1",
    "containing no characters from charset1 = \n\n",
    strcspn(string1, charset1));
  // ➁ strspn determines the length of the initial part of its first 
  // argument containing ONLY characters from its second argument
  printf("string1 = %s\ncharset1 = %s\n\n%s\n%s%zu\n\n", string1, charset1,
      "The length of the initial segment of string1",
      "containing only characters from charset1 = ",
      strspn(string1, charset1)); 

  puts("❻ search substring containing specified characters:");
  const char *strtarget = "This is a test"; 
  const char *charset2 = "beware"; 
  
  printf("%s\"%s\"\n'%c'%s \"%s\"\n\n",
    "Of the characters in ", charset2, *strpbrk(strtarget, charset2),
    " appears earliest in ", strtarget);

  puts("❼ search substring:");
  const char *source = "Beautiful is better than ugly."; 
  const char *goal = "better";

  printf("source = %s\ngoal = %s\n\n%s\n%s%s\n\n", source, goal, 
    "The remainder of source beginning with the",
    "first occurrence of goal is: ", strstr(source, goal));

  puts("❽ break string into tokens:");
  char code[] = "int x=3, y=4; int z = sqrt(x*x + y*y)";
  printf("The code to be tokenized is:\n%s\n\n", code);
  puts("The tokens are:");
  char *tokenPtr = strtok(code, " ");
  while (tokenPtr != NULL)
  {
    printf("%s\n", tokenPtr);
    tokenPtr = strtok(NULL, " ");
  }  
} 
```

🔭 Explore
---
- [Functions for string manipulation](https://en.cppreference.com/w/c/string/byte)


Memory functions
---
```c
#include <stdio.h>
#include <string.h>

int main(void) {
   puts("❶ copy memory:");
   char s1[17] = ""; 
   char s2[] = "Explicit is better than implicit."; 
   memcpy(s1, s2, 17); 
   puts("After s2 is copied into s1 with memcpy, s1 contains:");
   puts(s1); puts("");

   puts("❷ move memory:");
   char x[] = "Home Sweet Home";    
   printf("The string in array x before memmove is: %s\n", x); 
   printf("The string in array x after memmove is: %s\n", 
      (char *) memmove(x, &x[5], 10));
   puts("");

   puts("❸ compare memory:");
   char sa[] = "highland"; 
   char sb[] = "hilarious";       
   printf("sa = %s\ns2 = %s\n\n%s%2d\n%s%2d\n%s%2d\n", sa, sb,
      "memcmp(sa, sb, 2) = ", memcmp(sa, sb, 2),
      "memcmp(sa, sb, 7) = ", memcmp(sa, sb, 7),
      "memcmp(sb, sa, 7) = ", memcmp(sb, sa, 7));
   puts("");

   puts("❹ search character memory:");
   const char *s = "Simple is better than complex."; 
   printf("The remainder of s after character 'r' is found is \"%s\"\n",
      (char *) memchr(s, 't', 16));
   puts("");

   puts("❺ set memory:");
   char string1[15] = "Errors should never pass silently.";    
   printf("string1 = %s\n", string1);
   printf("string1 after memset = %s\n", (char *) memset(string1, 'b', 7)); 
} 
```

🔭 Explore
---
- [Functions for memory manipulation](https://en.cppreference.com/w/c/string/byte)


Miscelaneous string functions
---
```c
#include <stdio.h>
#include <string.h>

int main(void) {
  puts("❶ Find string length:");
  const char *string1 = "Flat is better than nested.";
  const char *string2 = "beast";
  const char *string3 = "beauty";  
  printf("%s\"%s\"%s%zu\n%s\"%s\"%s%zu\n%s\"%s\"%s%zu\n\n",
    "The length of ", string1, " is ", strlen(string1),
    "The length of ", string2, " is ", strlen(string2),
    "The length of ", string3, " is ", strlen(string3));

  puts("❷ Show error message:");
  printf("Error code 2 means %s\n", strerror(2));   
} 
```

🔭 Explore
---
- [Miscelaneous string functions](https://en.cppreference.com/w/c/string/byte)