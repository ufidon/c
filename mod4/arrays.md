__Arrays__

_chtp9e ch6_

[Arrays](https://en.cppreference.com/w/c/language/array)
---
- An array is a group of elements of the same type stored contiguously in memory
  - e.g. _the heights of 5 persons_:
    - `unsigned char height[5] = {160, 165, 172, 168, 170};` 
  - array name: `height` 
  - type: `unsigned char` 
  - total number of elements: `5`
  - initializer list: `{160, 165, 172, 168, 170}`
  - accessing elements: `height[0], height[1],..., height[4]`
    - by position number, subscript, or index
    - how about `height[5], height[-1]`, etc?
      - causing out of range exception
    - array elements can be used as normal variables
    ```c
    height[3] = 150;
    unsigned char average = (height[0]+height[1]+height[2]+height[3]+height[4])/5;
    printf("height list: %d,%d,%d,%d,%d\n",height[0],height[1],height[2],height[3],height[4]);
    ``` 
- A single piece of data is called a _scalar_    
  - Each element of a one dimensional array is a scalar


❓Question
---
- Find the precedence of the `array subscripting operator []`
  - in the [highest group](https://en.cppreference.com/w/c/language/operator_precedence)


Print arrays
---
```c
#include <stdio.h>
#define PERSON_NUMBER 5 

int main(void) {
   
   int height[PERSON_NUMBER] = {160, 165, 172, 168, 170}; 
   // ❶ print header line                                    
   printf("%7s%11s\n", "Person", "Height/cm");
   // ❷ iteratively print each element
   for (size_t i = 0; i < PERSON_NUMBER; ++i) {   
      printf("%7zu%11d\n", i, height[i]);
   } // ❸ %zu for type size_t defined in <stddef.h>
}
```


Define arrays
---
- `type arrayName[length];`
```c
float weight[5];
unsigned char age[5];
double worth[5];

#define PERSON_NUMBER 5 // define a symbolic constant. ❗no ;
int age[PERSON_NUMBER];
```

Initialize arrays
---
```c
// ➀ by initializer list
// ❶ full initialization
int a[5] = {160, 165, 172, 168, 170};
// ❷ explicit initialization with implicit initialization
int a[5] = {160, 165}; // equivalent to
int a[5] = {160, 165, 0, 0, 0};
// ❎ compilation error: more than needed
int w[2] = {1, 2, 3};
// ✅ let the initializer list determine the length
int w[] = {1, 2, 3};

// ➁ by loop for regular numbers
int even[5];
for (size_t i=0; i<5; ++i){
  even[i] = i*2;
}
```

Common operations on arrays
---
- print an array
  - `for(int i=0; i<SIZE; ++i) printf("%d ", a[i]);`
- filter an array
  - `for(int i=0; i<SIZE; ++i) if(filter(a[i])) printf("%d ", a[i]);`
  - e.g. print elements at even location
    ```c
    for(int i=0; i<SIZE; ++i)
      if(i%2 == 0) printf("%d ", a[i]);
    ``` 
    - how about printing elements at odd location?
- sum an array
  ```c
  int sum = 0;
  for(int i=0; i<SIZE; ++i) sum += a[i];
  ``` 


Applications of arrays
---
- 🅰 summarize survey results
```c
#include <stdio.h>
#define RESPONSES_SIZE 20 
#define FREQUENCY_SIZE 6 // rating scale 1-5, 0-th element wasted

int main(void) {
   int responses[RESPONSES_SIZE] = 
      {1, 2, 5, 4, 3, 5, 2, 1, 3, 1, 4, 3, 3, 3, 2, 3, 3, 2, 2, 5};

   int frequency[FREQUENCY_SIZE] = {0};
   
   for (size_t answer = 0; answer < RESPONSES_SIZE; ++answer) {
      ++frequency[responses[answer]]; // [] has higher precedence than ++
   } 
   printf("%s%12s\n", "Rating", "Frequency");
   
   for (size_t rating = 1; rating < FREQUENCY_SIZE; ++rating) {
      printf("%6zu%12d\n", rating, frequency[rating]);
   } 
} 
```

📝 Practice
---
- rewrite the survey program without wasting the 0-th element

- 🅱 Graph array elements with a horizontal bar chart
```c
#include <stdio.h>
#define SIZE 5

int main(void) {
   int n[SIZE] = {19, 3, 15, 7, 11};

   printf("%s%13s%17s\n", "Element", "Value", "Bar Chart");

   for (size_t i = 0; i < SIZE; ++i) {
      printf("%7zu%13d%8s", i, n[i], "");

      for (int j = 1; j <= n[i]; ++j) { 
         printf("%c", '*');                             
      }                                                 
      puts(""); 
   } 
} 
```

🕱 Challenge
---
- Could you draw a vertical bar chart for array elements?


- 🅲 Game simulation
  - Roll a die millions of times and summarize the results

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 7 // face dots 1-6, 0-th element wasted
#define ROLLING_TIMES 5000000

int main(void)
{
   srand(time(NULL));

   int frequency[SIZE] = {0};

   for (int roll = 1; roll <= ROLLING_TIMES; ++roll)
   {
      size_t face = 1 + rand() % 6;
      ++frequency[face];
   }

   printf("%s%17s\n", "Face", "Frequency");

   for (size_t face = 1; face < SIZE; ++face)
   {
      printf("%4zu%17d\n", face, frequency[face]);
   }
}
```  

📝 Practice
---
- rewrite the game simulation without wasting the 0-th element


- 🅳 Manipulate strings with character arrays
  - Each string ends with an implicit invisible null character '`\0`'
  - Popular ways to initialize a character array
    - with a string: `char str[] = "Hello";`
    - with a list of characters: `char str[] = {'H','e','l','l','o','\0'};`
    - with _scanf_: `char str[6]; scanf("%5s", str);`
  - Print a character array representing a string
    - `printf("%s\n", str);`

```c
#include <stdio.h>
#define SIZE 20

int main(void) {
   char state[SIZE] = ""; 
   char capital[] = "Tallahassee"; 

   printf("%s", "Enter a state name (no longer than 19 characters): ");
   scanf("%19s", state); 

   printf("state is: %s\ncapital is: %s\n", state, capital);
   puts("print state characters separated by space:");     

   for (size_t i = 0; i < SIZE && state[i] != '\0'; ++i) {
      printf("%c ", state[i]);                            
   }                                                        

   puts("");
} 
```


Static Local Arrays vs. Automatic Local Arrays
---
```c
#include <stdio.h>

void staticArrayInit(void);
void automaticArrayInit(void);

int main(void)
{
   puts("First call to each function:");
   staticArrayInit();
   automaticArrayInit();

   puts("\n\nSecond call to each function:");
   staticArrayInit();
   automaticArrayInit();
   puts("");
}

void staticArrayInit(void)
{ // ❶ retain values across function call
  static int array1[3];

  puts("\nValues on entering staticArrayInit:");

  for (size_t i = 0; i <= 2; ++i)
  {
    printf("array1[%zu] = %d  ", i, array1[i]);
  }

  puts("\nValues on exiting staticArrayInit:");

  for (size_t i = 0; i <= 2; ++i)
  {
    printf("array1[%zu] = %d  ", i, array1[i] += 5);
  }
}

void automaticArrayInit(void)
{ // ❷ exist temporarily when the function is active
  int array2[3] = {1, 2, 3};

  puts("\n\nValues on entering automaticArrayInit:");

  for (size_t i = 0; i <= 2; ++i)
  {
    printf("array2[%zu] = %d  ", i, array2[i]);
  }

  puts("\nValues on exiting automaticArrayInit:");

  for (size_t i = 0; i <= 2; ++i)
  {
    printf("array2[%zu] = %d  ", i, array2[i] += 5);
  }
}
```


Passing Arrays to Functions
---
```c
int a[SIZE];
initialize(a, SIZE); // prototype: initialize(int a[], size_t size);
```
- An array name is the address of the array
  ```c
  #include <stdio.h>

  int main(void)
  {
    char array[5] = "";

    printf("array = %p\n&array[0] = %p\n&array = %p\n",
            array, &array[0], &array);
  }  
  ```


Difference Between Passing an Entire Array and Passing an Array Element
---
```c
#include <stdio.h>
#define SIZE 5

void modifyArray(int b[], size_t size);
void modifyElement(int e);

int main(void)
{
   int a[SIZE] = {0, 1, 2, 3, 4};

   puts("Effects of passing entire array by reference:\n\nThe "
        "values of the original array are:");

   for (size_t i = 0; i < SIZE; ++i)
   {
      printf("%3d", a[i]);
   }

   puts("");

   modifyArray(a, SIZE);
   puts("The values of the modified array are:");

   for (size_t i = 0; i < SIZE; ++i)
   {
      printf("%3d", a[i]);
   }

   printf("\n\n\nEffects of passing array element "
          "by value:\n\nThe value of a[3] is %d\n",
          a[3]);

   modifyElement(a[3]);

   printf("The value of a[3] is %d\n", a[3]);
}

void modifyArray(int b[], size_t size)
{

   for (size_t j = 0; j < size; ++j)
   {
      b[j] *= 2;
   }
}

void modifyElement(int e)
{
   e *= 2;
   printf("Value in modifyElement is %d\n", e);
}
```

Using const to Prevent Functions from Modifying Array Elements
---
```c
void dontModifyMe(const int a[]){
  a[0] *= 2; // raise a compilation error
}
```

Sort arrays
---
- [bubble sort](../chtp9ecode/ch06/fig06_12.c)


Search arrays
---
- [Linear search](../chtp9ecode/ch06/fig06_14.c)
- [binary search](../chtp9ecode/ch06/fig06_15.c)


Application in data science: survey data analysis
---
- Find the _mean, median and mode_ of a data set
- [survey statistics](../chtp9ecode/ch06/fig06_13.c)


Multidimensional arrays
---
- Definition and initialization
```c
#include <stdio.h>

void printArray(int a[][3]);

int main(void)
{
  int array1[2][3] = {{1, 2, 3}, {4, 5, 6}};
  puts("Values in array1 by row are:");
  printArray(array1);

  int array2[2][3] = {{1, 2, 3}, {4, 5}};
  puts("Values in array2 by row are:");
  printArray(array2);

  int array3[2][3] = {{1, 2}, {4}};
  puts("Values in array3 by row are:");
  printArray(array3);
}

void printArray(int a[][3])
{
  for (size_t i = 0; i <= 1; ++i)
  {
    for (size_t j = 0; j <= 2; ++j)
    {
        printf("%d ", a[i][j]);
    }
    printf("\n");
  }
}
```
- In C, multidimensional arrays are organized row by row, or row-wise


Popular operations on multidimensional arrays
---
```c
// ❶ Update one row
for(int col=0; col<ROW_LENGTH; ++col){
  a[1][col] = 7;
}

// ❷ Sum all elements
int sum = 0;
for(int r=0; r<COL_LENGTH; ++r){
  for(int c=0; c<ROW_LENGTH; ++c){
    sum += a[r][c];
  }
}
```


- ❸ [find the minimum, maximum and average](../chtp9ecode/ch06/fig06_17.c)


Variable-Length Arrays (VLAs)
---
- supported by gcc and clang but not Visual C++
- the length of a VLA is determined during runtime
- [a example](../chtp9ecode/ch06/fig06_18.c)
