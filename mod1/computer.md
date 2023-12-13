__Introduction to Computers__
_chtp9e ch1_

What is a [computer](https://en.wikipedia.org/wiki/Computer)?
---
- a machine consists of hardware, data and software 
- can be programmed to carry out tasks automatically
  - the sequences of instructions used to process data
    - are called computer programs (or simply programs)
    - written by computer programmers
- connects and communicates to other computers through network
- with specific peripherals for specific usage


How fast are computers developing?
---
- [Moore's law](https://en.wikipedia.org/wiki/Moore%27s_law) is the observation that 
  - the number of transistors in an microchip doubles about every two years


How is a computer organized from [components](https://en.wikipedia.org/wiki/Computer_hardware)?
---
- computer components can be categorized into several logic units or sections

| Logic units or sections | Function | Examples |
| --- | --- | --- |
| Input units | Acquire and receive information |  ▶️ keyboard, touch screen, mice, touchpads<br/> ▶️ microphone, camera, scanner<br/> ▶️ GPS, compass, thermometer, gyroscope, accelerometer |
| Output units | present or output processed information | ▶️ screen, printer <br/> ▶️ speaker, beeper <br/> ▶️ activators such as the steering wheel of autonomous vehicles  |
| Memory units | ▶️ hold data for processing <br/>▶️ hold software for running | DDR RAM |
| Secondary Storage Units | save data and software persistently | SSD, USB drive, DVD |
| Central processing units (CPU) |  coordinates and supervises the operation of the other units | multicore processors |
| Arithmetic and logic units (ALU) | perform arithmetic and logic operations | part of CPU |

- many devices can be used for both input and output such as network communication devices


💡 Demo
---
- Explore the devices on a computer
  - Device manager
  - [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)
- Explore the software on a computer
  - system information
  - [Sysinternals](https://learn.microsoft.com/en-us/sysinternals/)


❓ Questions
---
1. The observed approximate trend that computers' capacities doubled every one or two years is called _______?
2. Does the information in the memory survive power off?
3. A CPU integrated multiple processors is called ___________ processors?

---

How data are organized?
---
- in a data hierarchy from the simplest data items _bits_ to complex structures _files_ and _databases_
- A _bit_, or binary digit, can represent 2 possible values 0 or 1
- A _nibble_ has 4 bits, can represent $2^4 = 16$ possible values
- A _byte_ has 8 bits, can represent $2^8 = 256$ possible values


Characters
---
- programs and data items are written in characters such as
  - decimal digits (0-9)
  - letters (A-Z and a-z)
  - punctuations (or special symbols)
- C programs 
  - use the ASCII (American Standard Code for Information Interchange) character set by default
  - support Unicode characters composed of 1-4 bytes


Fields, records, files, databases
---
- A field is composed of characters or bytes that convey meaning
  - such as a person's name, height, weight, etc.
- A record consists of several related fields
  - such as a person consists of name, height, weight, etc.
- A file is a group of related records
  - can contain arbitrary data in arbitrary formats
- A database is a collection of data organized for easy access and manipulation
  - the most popular model is the relational database
    - consists of a set of tables and constraints


📝 Practice
---
- how to measure the size of data?
  - [Orders of magnitude](https://en.wikipedia.org/wiki/Orders_of_magnitude_(data))
  - [Binary prefix](https://en.wikipedia.org/wiki/Binary_prefix)


❓ Questions
---
1. A binary digits is called ________, the smallest data item, assumes one of two values.
2. Can a file be viewed simply as a sequence of bytes?
3. The most popular database model is ____________ database.

---


The three types of programming languages
---
- sort by the distance away from hardware
  - Machine language (ML)
    - ISA (instruction set architecture) dependent, simply machine dependent
    - understand by the specific machines
    - usually denoted in hexadecimal numbers
  - Assembly language (AL)
    - mnemonic of machine language, ML dependent
    - translated into ML through assembler
  - High-level language (HL)
    - close to human language
    - compiled HL can be compiled into AL or ML through compilers
      - such as C, C++
    - interpreted HL can be compiled into byte code of virtual machines for interpretation
      - such as Python, Java, C#


💡Demo
---
- use the following program
  ```c
  #include <stdio.h>

  int main(){
    printf("Hello everyone, welcome to C!\n");

    return 0;
  }
  ```
- show ML, AL and C in vs code
  - set a breakpoint in a C program
  - start debug
  - right-click a line to open the disassembly view


❓ Questions
---
1. Translator programs called __________ convert AL programs to ML at computer speeds.
2. _________ execute HL programs directly, usually slower than compiled programs.
3. Do HLs let you write instructions like normal English and contain commonly used mathematical notations? 

---

Operating system (OS)
---
- system software that 
  - manages computer hardware and software resources 
  - provides common services for computer programs
- the core OS component is called the kernel
- popular OSes
  - Windows, Linux, macOS, Android, iOS
- open source software 
  - makes its source code publicly available
  - increases productivity 
  - leads to the flourish of software


❓Questions
---
1. Linux is an ______ OS but Windows is a proprietary OS.
2. Is open-source code checked by larger audience than proprietary code?
3. Does Android have higher market share than iOS?

---

The C programming language
---
- evolved from two earlier languages BCPL and B
- became well-known for writing UNIX OS in C
- mostly hardware-independent, i.e. portable to most computers
- used to develop systems that demand performance such as
  - OSes, embedded systems, real-time systems, communication systems
- many standards by American National Standards Institute (ANSI) and International Standards Organization (ISO)
  - ANSI C and ISO C --> C99 (1999) --> C11 (2011) --> C18 (previously known as C17) --> C23


❓Questions
---
1. C evolved from ________ and __________.
2. Is C program portable to most computers?


C libraries
---
- consist of functions and variables for _software reuse_
  - Don't reinvent the wheel
- C Standard Library is supplied by the C compiler
  - used for common basic tasks
- Open-source C libraries for various purposes


❓Questions
---
1. The rich collection of existing functions used by most C programmers is called ____________.
2. Using existing code instead of reinventing the wheel is called ___________.

---

Typical C program development environment
---
- typically in an IDE (integrated development environment) such as
  - Visual Studio
- let programmers to go through 6 phases in one place
  1. create a C project, edit source code
  2. preprocess the macros in C source code
  3. compile the C source code into object code
  4. link the object code with static libraries to produce the executable file
  5. load the executable file, may link shared libraries dynamically
  6. execute the executable file
- Errors occurred at phase 2,3 are called _syntax errors_
- Errors occurred at phase 4,5 are called _link errors_
- Errors occurred at phase 6 are called _runtime errors_ or _execution-time errors_


💡Demo
---
- [Using GCC with MinGW](https://code.visualstudio.com/docs/cpp/config-mingw)
- Go through the 6 phases of developing a C program
  - use [guessing number](../chtp9ecode/ch01/randomized_version/GuessNumber.c)

```bash
# 1. create a C project, edit the source code
# 2. preprocess
gcc -E GuessNumber.c

# 3. compile
# 3.1 convert into AL (optional)
gcc -S GuessNumber.c

# 3.2 convert into object code ML
gcc -c GuessNumber.c

# 4. link, quite complex
gcc -v GuessNumber.c  -o GuessNumber # show the complexity

# 5. load and execute
./GuessNumber
```
- Use online C compilers
  - [onlinegdb](https://www.onlinegdb.com/)


📝 Extra practice
---
- [Configure VS Code for Microsoft C++](https://code.visualstudio.com/docs/cpp/config-msvc)
- [clangd](https://clangd.llvm.org/installation.html)