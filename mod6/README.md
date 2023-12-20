__File processing__

_chtp9e ch11_

Files
---
- enable long-term data retention on secondary storage devices
- each file can be viewed as a sequential stream of bytes
  - ends with an end-of-file marker (EOF)
- every running program is associated with three streams automatically
  - The _standard input_ stream receives input from the keyboard
  - The _standard output_ stream displays output on the screen
  - The _standard error_ stream displays error messages on the screen


File structure
---
- Opening a file returns a pointer to a FILE structure
  - this structure includes a _file descriptor_, 
    - an integer index into the OS maintained array named _open file table_
    - each table entry contains a _file control block (FCB)_
- the predefined FILE pointers to the three standard stream are
  - _stdin, stdout_ and _stderr_


📝 Practice
---
1. [Create a sequential-access file](../chtp9ecode/ch11/fig11_01.c)
   1. define a pointer to a FILE structure
   2. open a file with `fopen`
   3. check for the EOF indicator with `feof`
   4. write to the file with `fprintf`
   5. close the file with `fclose`
2. [Read data from a sequential-access file](../chtp9ecode/ch11/fig11_02.c)
   1. reset the file position pointer with `rewind`
   2. [credit inquiry program](../chtp9ecode/ch11/fig11_03.c)
3. [Create a random-access file](../chtp9ecode/ch11/fig11_04.c)
4. [Write data randomly to a random-access file](../chtp9ecode/ch11/fig11_05.c)
5. [Read data from a random-access file](../chtp9ecode/ch11/fig11_06.c)
6. [Create a transaction-processing program](../chtp9ecode/ch11/fig11_07.c)


🔭 Explore: 
---
- [File-processing functions](https://cplusplus.com/reference/cstdio/)
  - [File access flags](https://cplusplus.com/reference/cstdio/fopen/)


💀 ☠ 🕱 Adventure
---
- [Free e-books on Gutenberg for NLP(natural language processing)](https://www.gutenberg.org)
- [GNU Scientific Library and gnuplot](https://www.gnu.org/software/gsl/)
- [Weather data on The National Oceanic and Atmospheric Administration (NOAA)](http://www.noaa.gov)
  - [OpenWeatherMap](https://openweathermap.org/)
- [Open-Source libcurl Library](https://github.com/curl/curl)
- [Open Source cJSON Library](https://github.com/DaveGamble/cJSON)
- [self-hostable web applications](https://github.com/awesome-selfhosted/awesome-selfhosted)
