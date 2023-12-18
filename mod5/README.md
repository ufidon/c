__Pointers__

_chtp9e ch7_


Pointers
---
- are variables whose values are memory addresses
  - A pointer points to a variable if it contains the address of that variable
  - referencing that variable's value by this pointer is called indirection or dereferencing
- capabilities
  - pass parameters by references
  - pass functions between functions
  - manipulate strings and array efficiently
  - create and manipulate dynamic data structures


Pointer Variable Definitions and Initialization
---
```c
// 🅐 definition
int *p; // ❶ p is a pointer to int

int *countPtr, count; // equivalent to
int *countPtr; int count;

// 🅑 initialization
int *countPtr = &count;
int *countPtr = 0; // equivalent to
int *countPtr = NULL; // defined in <stddef.h> as ((void*)0)
```


Pointer operators
---
```c
#include <stdio.h>

int main(void)
{
   int a = 7;
   int *np = NULL;
   int *aPtr = &a;

   printf("Address of a is %p\nValue of aPtr is %p\n\n", &a, aPtr);
   printf("Value of a is %d\nValue of *aPtr is %d\n\n", a, *aPtr);
   printf("Showing that * and & are complements of each other\n");
   printf("&*aPtr = %p\n*&aPtr = %p\n", &*aPtr, *&aPtr);
}
```
- address `&` operator returns the address of its operand
- indirection `*` operator, or dereferencing operator
  - applies to a pointer operand to get the value of the object to which the pointer points
  - dereferencing an uninitialized pointer may cause fatal runtime error
- operator `&` and `*` are in the [second highest precedence group](https://en.cppreference.com/w/c/language/operator_precedence)


Pass arguments to functions
---
```c
#include <stdio.h>

int cubeByValue(int);
void cubeByReference(int *);

int main(void)
{
   int number = 5, cube;

   printf("Pass by value:\n");
   printf("The original value of number is %d", number);
   cube = cubeByValue(number);
   printf("\nThe new value of number is %d\n", number);

   printf("\nPass by reference:\n");
   printf("The original value of number is %d", number);
   cubeByReference(&number);
   printf("\nThe new value of number is %d\n", number);   
}

int cubeByValue(int n)
{
   return n * n * n;
}

void cubeByReference(int *nPtr)
{
   *nPtr = *nPtr * *nPtr * *nPtr;
}
```
- in formal function parameters,
  - `int a[]` is equivalent to `int *a`
    - `const int a[]` to `const int *a`
- Four ways to pass to a function a pointer to data
  - 🅐 a non-constant pointer to non-constant data
  - 🅑 a non-constant pointer to constant data
  - 🅒 a constant pointer to non-constant data
  - 🅓 a constant pointer to constant data

```c
#include <ctype.h>
#include <stdio.h>

// 🅐 a non-constant pointer to non-constant data
void convertToUppercase(char *sPtr);

int main(void)
{
  char string[] = "cHaRaCters and $32.98";

  printf("The string before conversion is: %s\n", string);
  convertToUppercase(string);
  printf("The string after conversion is: %s\n", string);
}

void convertToUppercase(char *sPtr)
{
  while (*sPtr != '\0')
  {
    *sPtr = toupper(*sPtr);
    ++sPtr;
  }
}
```

```c
#include <stdio.h>
// 🅑 a non-constant pointer to constant data
void printCharacters(const char *sPtr);

int main(void)
{
  char string[] = "print characters of a string";

  puts("The string is:");
  printCharacters(string);
  puts("");
}

void printCharacters(const char *sPtr)
{
  for (; *sPtr != '\0'; ++sPtr)
  {
    printf("%c", *sPtr);
  }
}
```
- Trying to modify constant data causes compilation error
  ```c
  void f(const int *xPtr) {
    *xPtr = 100; // ⚠️ error: cannot modify a const object
  }   
  ```


Pass structures vs. arrays
---
- Passing structures by pointers to constant data obtains 
  - the performance of pass-by-reference 
  - and the security of pass-by-value
- A constant pointer to non-constant data always points to the same memory location
  - but the data at that location can be modified through the pointer
   ```c
   // 🅒 a constant pointer to non-constant data
   int *const ptr = &x;
   *ptr = 17; // allowed: *ptr is not const
   ptr = &y; // error: ptr is const; cannot assign new address
   ```
  - This is the default for an array name
    -  which is a constant pointer to the array’s first element
-  A constant pointer to constant data always points to the same memory location 
   - and the data at that memory location cannot be modified
   ```c
   // 🅓 a constant pointer to constant data
   const int *const ptr = &x; // initialization is OK
   *ptr = 17; // error: *ptr is const; cannot assign new value
   ptr = &y; // error: ptr is const; cannot assign new address
   ```  


- Bubble Sort Using Pass-By-Reference
```c
#include <stdio.h>
#define SIZE 10

void bubbleSort(int *const array, size_t size); 

int main(void)
{
  int a[SIZE] = {2, 6, 4, 8, 10, 12, 89, 68, 45, 37};
  puts("Data items in original order");

  for (size_t i = 0; i < SIZE; ++i)
  {
    printf("%4d", a[i]);
  }

  bubbleSort(a, SIZE); 
  puts("\nData items in ascending order");
  
  for (size_t i = 0; i < SIZE; ++i)
  {
    printf("%4d", a[i]);
  }

  puts("");
}

void bubbleSort(int *const array, size_t size)
{
  // swap is used only in bubbleSort
  void swap(int *element1Ptr, int *element2Ptr);  

  for (int pass = 0; pass < size - 1; ++pass)
  {      
    for (size_t j = 0; j < size - 1; ++j)
    {
        
      if (array[j] > array[j + 1])
      {
        swap(&array[j], &array[j + 1]);
      }
    }
  }
}

void swap(int *element1Ptr, int *element2Ptr)
{
  int hold = *element1Ptr;
  *element1Ptr = *element2Ptr;
  *element2Ptr = hold;
}
```

sizeof Operator
---
- An unary operator to determine an object’s or type’s size in bytes

```c
#include <stdio.h>

int main(void) {
  char c = '\0';           
  short s = 0;         
  int i = 0;       
  long l = 0;         
  long long ll = 0;         
  float f = 0.0F;        
  double d = 0.0;         
  long double ld = 0.0;   
  int array[20] = {0}; 
  int *ptr = array; 

  printf("    sizeof c = %2zu\t       sizeof(char) = %2zu\n", 
    sizeof c, sizeof(char));
  printf("    sizeof s = %2zu\t      sizeof(short) = %2zu\n", 
    sizeof s, sizeof(short));
  printf("    sizeof i = %2zu\t        sizeof(int) = %2zu\n", 
    sizeof i, sizeof(int));
  printf("    sizeof l = %2zu\t       sizeof(long) = %2zu\n", 
    sizeof l, sizeof(long));
  printf("   sizeof ll = %2zu\t  sizeof(long long) = %2zu\n", 
    sizeof ll, sizeof(long long));
  printf("    sizeof f = %2zu\t      sizeof(float) = %2zu\n", 
    sizeof f, sizeof(float));
  printf("    sizeof d = %2zu\t     sizeof(double) = %2zu\n",
    sizeof d, sizeof(double));
  printf("   sizeof ld = %2zu\tsizeof(long double) = %2zu\n",
    sizeof ld, sizeof(long double));
  printf("sizeof array = %2zu\n  sizeof ptr = %2zu\n", 
    sizeof array, sizeof ptr);
} 
```
- Get array size
```c
#include <stdio.h>
#define SIZE 20

size_t getSize(const float *ptr); 

int main(void){
  float array[SIZE]; 

  printf("Number of bytes in the array is %zu\n", sizeof(array));
  printf("Number of elements in array is %zu\n", sizeof(array)/sizeof(array[0]));
  printf("Number of bytes returned by getSize is %zu\n", getSize(array));
} 

size_t getSize(const float *ptr) {
  return sizeof(ptr);
} 
```


Pointer Arithmetic Operators
---
```c
#include <stdio.h>
#define SIZE 5

int main(void)
{
   int b[] = {10, 20, 30, 40, 50};

   puts("❶ Aiming a Pointer at an Array");
   int * const pheader = b, * const ptail = &b[SIZE-1];
   printf("b = %p\npheader = %p\nptail = %p\n", b, pheader, ptail);
   printf("\n");

   puts("❷ Assigning Pointers to One Another");
   puts("   must be the same type");
   int *p = pheader;
   printf("p = pheader = %p\n\n", p);


   puts("❸ Adding an Integer to a Pointer");
   for (int i = 0; i < SIZE; i++)
   {
      p = pheader + i;
      printf("p=%p+%d = %p, *p = %d\n", pheader, i, p, *p);
   }
   printf("\n");
   
   puts("❹ Subtracting an Integer from a Pointer");
   for (int i = 0; i < SIZE; i++)
   {
      p = ptail - i;
      printf("p=%p-%d = %p, *p = %d\n", ptail, i, p, *p);
   }
   printf("\n");
   
   
   puts("❺ Incrementing a Pointer");
   p = pheader;
   do
   {
      printf("p = %p, *p = %d\n", p, *p);
   } while (p++ < ptail);
   printf("\n");

   puts("❻ Decrementing a Pointer");
   p = ptail;
   do
   {
      printf("p = %p, *p = %d\n", p, *p);
   } while (p-- > pheader);
   puts("");

   puts("❼ Subtracting One Pointer from Another");
   printf("  The array has %ld elements.\n\n", ptail-pheader+1);


   puts("❽ Comparing Pointers");
   for (p = pheader; p<= ptail; ++p)
   {
      printf("p = %p, *p = %d\n", p, *p);
   }
   puts("");
   
   puts("❾ Pointer to void");
   p = 0; // or NULL, which is defined as (void*)0
   printf("p = %p\n\n", p);
   puts(" *p = 3; //⚠️ Dereferencing a void * pointer is a syntax error");
   puts(" because a void * contains a memory location for an unknown type\n");

   puts("❿ Pointer to void is a generic pointer \n"
   "  that can represent any pointer type.\n"
   "  All pointer types can be assigned to a void *\n"
   "  and a void * can be assigned a pointer of any type (including another void *).");
   void * pvoid = pheader;
   if(p==NULL) p = pvoid;
   printf("pvoid = pheader = %p, p = pvoid = %p\n", pvoid, p);
}
```
- allowed arithmetic operations
  - incrementing `++` or decrementing `--`,
  - adding an integer to a pointer `+ or +=`,
  - subtracting an integer from a pointer `- or -=`, and
  - subtracting one pointer from another is meaningful only 
    - when both pointers point into the same array
- Pointer arithmetic on pointers that do not refer to array elements is a logic error


Manipulate arrays with array name and pointer
---
```c
#include <stdio.h>
#define SIZE 5

int main(void)
{
  int b[] = {10, 20, 30, 40, 50};
  int * const pb = b, *pheader = &b[0], *ptail = &b[SIZE-1];

  puts("➊ Array b printed with:\nArray subscript notation");

  for (size_t i = 0; i < SIZE; ++i)
  {
    printf("b[%zu] = %d\n", i, b[i]);
  }

  puts("\n➋ Pointer/offset notation where the pointer is the array name");

  for (size_t offset = 0; offset < SIZE; ++offset)
  {
    printf("*(b + %zu) = %d\n", offset, *(b + offset));
  }

  puts("\n➌ Pointer subscript notation");

  for (size_t i = 0; i < SIZE; ++i)
  {
    printf("pb[%zu] = %d\n", i, pb[i]);
  }

  puts("\n➍ Pointer/offset notation");

  for (size_t offset = 0; offset < SIZE; ++offset)
  {
    printf("*(pb + %zu) = %d\n", offset, *(pb + offset));
  }

  // b += 2; // ⚠️ ➎ error: array name is a constant pointer 
}
```

Copy strings with arrays and pointers
---
- the target string must be no shorter than the source string
```c
#include <stdio.h>
#define SIZE 10

void copy1(char *const, const char *const);
void copy2(char *, const char *);

int main(void)
{
  char string1[SIZE];
  char *string2 = "Hello";
  
  copy1(string1, string2);
  printf("string1 = %s\n\n", string1);

  char string3[SIZE];
  char string4[] = "Good Bye";
  
  copy2(string3, string4);
  printf("string3 = %s\n\n", string3);
}

void copy1(char *const s1, const char *const s2)
{
  puts("❶ copy with array subscript notation:");
  for (size_t i = 0; (s1[i] = s2[i]) != '\0'; ++i);
}

void copy2(char *s1, const char *s2)
{
  puts("❷ copy with pointers and pointer arithmetic:");
  for (; (*s1 = *s2) != '\0'; ++s1, ++s2);
}
```
- ❓ Question
  1. How many bytes are wasted in string1 and string3?
  2. Rewrite the for loops with while loop in the two copy functions


Arrays of pointers
---
- commonly used for array of strings
  - named string array
```c
const char *suit[4] = {"Heart", "Diamond", "Club", "Spade"};
```
-  a char * array is _fixed in size_ 
   -  but it can point to character strings of _any length_

📝 Practice
---
- [Card shuffling and dealing with 2-dimensional array](../chtp9ecode/ch07/fig07_16.c)


Function pointers
---
-  a function’s name is the starting address of its code in memory
-  A pointer to a function contains the address of the function in memory
-  Pointers to functions can be 
   -  passed to functions
   -  returned from functions
   -  stored in arrays
   -  assigned to other function pointers of the same type 
   -  compared with one another for equality or inequality


📝 Practicd
---
- sorting in ascending or descending order
```c
#include <stdio.h>
#define SIZE 10

void bubbleSort(int work[], size_t size, int (*compare)(int a, int b));
int ascending(int a, int b);
int descending(int a, int b);

int main(void)
{
  int a[SIZE] = {2, 6, 4, 8, 10, 12, 89, 68, 45, 37};

  printf("%s", "Enter 1 to sort in ascending order,\n"
              "Enter 2 to sort in descending order: ");
  int order = 0;
  scanf("%d", &order);

  puts("\nData items in original order");

  for (size_t counter = 0; counter < SIZE; ++counter)
  {
    printf("%5d", a[counter]);
  }

  if (order == 1)
  {
    bubbleSort(a, SIZE, ascending);
    puts("\nData items in ascending order");
  }
  else
  {
    bubbleSort(a, SIZE, descending);
    puts("\nData items in descending order");
  }

  for (size_t counter = 0; counter < SIZE; ++counter)
  {
    printf("%5d", a[counter]);
  }

  puts("\n");
}

void bubbleSort(int work[], size_t size, int (*compare)(int a, int b))
{
  void swap(int *element1Ptr, int *element2ptr);

  for (int pass = 1; pass < size; ++pass)
  {

    for (size_t count = 0; count < size - 1; ++count)
    {

        if ((*compare)(work[count], work[count + 1]))
        {
          swap(&work[count], &work[count + 1]);
        }
    }
  }
}

void swap(int *element1Ptr, int *element2Ptr)
{
  int hold = *element1Ptr;
  *element1Ptr = *element2Ptr;
  *element2Ptr = hold;
}

int ascending(int a, int b)
{
  return b < a;
}

int descending(int a, int b)
{
  return b > a;
}
```

- A function pointer can be called in two ways
  1. `(*fun)(parameters)` dereferences the function pointer
  2. `fun(parameters)` uses fun as an actual function name


📝 Practice
---
- [Create a menu-driven system with function pointers](../chtp9ecode/ch07/fig07_18.c)


💀 ☠ 🕱 Adventure
---
- [raylib - a simple and easy-to-use library to enjoy videogames programming](https://www.raylib.com/)
- [Webots - an open-source, full-color, 3D, robotics simulator with console-game-quality graphics](https://cyberbotics.com)
