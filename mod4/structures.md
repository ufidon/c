__Structures, Unions, Bit Manipulation and Enumerations__

_chtp9e ch10_


[Structures](https://en.cppreference.com/w/c/language/struct)
---
```c
// ⓵ define structure types
struct Card // ❶ structure type (struct Card) and ❷ tag (Card)
{
  char face; // ❸ structure member
  char suit;
};

struct Person{
  char firstName[20];
  char lastName[20];
  int age;
  double salary;
}

// ⓶ define variable of structure types
struct Card mycard;
struct Card deck[52];

// or
struct Card{  // the tag name Card is optional here
  char face;
  chart suit;
}mycard, deck[52];

// ⓷ operations on structures
struct Card card = {}; // ❶ zero initialization
struct card cardJ = {'J', 'H'}; // ❷ initializer list
size_t s = sizeof(card); // ❸ 
struct Card card2 = card; // ❹ 
card.face = 'A'; // ❺
// ⚠️ comparing structures is NOT allowed
```
- collections of related variables under one name
  - variables may be of different types
  - while array contains only elements of the same type
- known as aggregates in the C standard
- derived data types
  - constructed using objects of other types


📝 Practice
---
- member accessing
```c
#include <stdio.h>

struct card
{
   char face;
   char suit;
};

int main(void)
{
   struct card myCard;

   myCard.face = 'A';
   myCard.suit = 'S';

   printf("%c of %c\n", myCard.face, myCard.suit);
}
```

typedef
---
-  enables creation of synonyms (or aliases) for previously defined types
  ```c
  typedef struct card Card;

  typedef struct{
    char face;
    char suit;
  } Card;

  typedef unsigned char Age;
  ```


Use structures with functions
---
-structures are passed to functions by value
   - create a structure with an array member to pass array by value
- shuffle and deal card
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define CARDS 52
#define FACES 13

struct card
{
    char face;
    char suit;
};

typedef struct card Card;

void fillDeck(Card  deck[],  char faces[],  char suits[]);
void shuffle(Card  deck[]);
void deal( Card  deck[]);

int main(void)
{
  Card deck[CARDS];

  char faces[] = {'A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'};
  char suits[] = {'H', 'D', 'C', 'S'};

  srand(time(NULL));

  fillDeck(deck, faces, suits);
  shuffle(deck);
  deal(deck);
}

void fillDeck(Card  deck[],  char faces[],
               char suits[])
{
  for (size_t i = 0; i < CARDS; ++i)
  {
    deck[i].face = faces[i % FACES];
    deck[i].suit = suits[i / FACES];
  }
}

void shuffle(Card  deck[])
{
  for (size_t i = 0; i < CARDS; ++i)
  {
    size_t j = rand() % CARDS;
    Card temp = deck[i];
    deck[i] = deck[j];
    deck[j] = temp;
  }
}

void deal( Card  deck[])
{
  for (size_t i = 0; i < CARDS; ++i)
  {
    printf("%5c of %-8c%c", deck[i].face, deck[i].suit,
            (i + 1) % 4 ? ' ' : '\n');
  }
}
```


[Unions](https://en.cppreference.com/w/c/language/union)
---
```c
#include <stdio.h>

union number
{
   int x;
   double y;
};

int main(void)
{
   union number value;

   value.x = 100;
   puts("Put 100 in the int member and print both members:");
   printf("int: %d\ndouble: %.2f\n\n", value.x, value.y);

   value.y = 100.0;
   puts("Put 100.0 in the double member and print both members:");
   printf("int: %d\ndouble: %.2f\n\n", value.x, value.y);
}
```
- a derived data type similar to struct but
- its members share the same memory
   - the amount of memory required to store a union is _implementation-dependent_


[Bitwise operators](https://en.cppreference.com/w/c/language/operator_arithmetic)
---
- Computers represent all data internally as sequences of bits
- bitwise operators are used to manipulate the bits of integral operands, 
  - both signed and unsigned
    - unsigned integers are typically used
  - machine-dependent


📝 Practice
---
- [Displaying an Unsigned Integer’s Bits](../chtp9ecode/ch10/fig10_04.c)
- [Using the Bitwise AND, Inclusive OR, Exclusive OR and Complement Operators](../chtp9ecode/ch10/fig10_05.c)
- [Using the Bitwise Left- and Right-Shift Operators](../chtp9ecode/ch10/fig10_06.c)


👁️ Review
---
- [Bitwise Assignment Operators](https://en.cppreference.com/w/c/language/operator_arithmetic)
- [C Operator Precedence](https://en.cppreference.com/w/c/language/operator_precedence)


[Bit fields](https://en.cppreference.com/w/c/language/bit_field)
---
- [Using Bit Fields to Represent a Card’s Face, Suit and Color](../chtp9ecode/ch10/fig10_07.c)
```c
#include <stdio.h>

enum months {                                                     
   JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC 
};                                                                
 
int main(void) {  
  const char *monthName[] = { "", "January", "February", "March", 
    "April", "May", "June", "July", "August", "September", "October",
    "November", "December" };
    
  for (enum months month = JAN; month <= DEC; ++month) {
    printf("%2d%11s\n", month, monthName[month]);
  }
}
```


Anonymous Structures and Unions
---
```c
// ❶ define
struct myStruct{
  int m1;
  int m2;

  struct { // anonymous struct
    int sm1;
    int sm2;
  };
};
// ❷ access member
struct myStruct s = {1,2,{3,4}};
s.m1 *= 2;
s.sm2 *= 3; // ⚠️
```