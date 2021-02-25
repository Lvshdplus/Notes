# GDB Manual

This note shows some basic use of GDB(GNU Project Debugger).

```c++
/* To use gdb, add '-g' flag when compiling */
$ g++ -g example.cpp -o main
  
/* use gdb to run executable file */
$ gdb ./main

/* visualize the file to debug */
(gdb) press ctrl+x then press a
  
/* run the program */
(gdb) run (r)
  
/* set breakpoint */
(gdb) break {function name | line number | crash} (b)
- function name: eg. break main
- line number: eg. break 7 (some specific line number)
- crash: eg. break crash (break at the code which causes segmentation fault)

/* execute the next instruction */
(gdb) next (n)

/* show the codes arround the breakpoint */
(gdb) list (l)
  
/* print the value of a specific variable */
(gdb) print (p)
  
/* up (down) find upstream (downstream) function */
(gdb) up | down

/* display */
(gdb) display {instruction}
- display the instruction evry time
- each variable displayed has a ID number
  
/* undisplay */
(gdb) undisplay {instruction ID number}
- undisplay the instruction we don not need anymore

/* backtrace the entire call stack */
(gdb) backtrace (bt)

/* step let us go into a function*/
(gdb) step (s)

/* run the codes until we reach next breakpoint */
(gdb) continue (c)

/* print the return value of a function */
(gdb) finish

/* watch some variable, program will stop until the variable is changed */
(gdb) watch {variable}

/* a table displays all breakpoints */
(gdb) info breakpoints


/** delete the specific breakpoint with ID
  * if no ID number entered, delete all breakpoints
  */
(gdb) delete [ID number] (d)

/* figure out the type of varible */
(gdb) whatis {varibale name} (what)

/** from now onw, record all the instructions
  * we entered, thus we can undo instructions
  */
(gdb) target record-full

/** undo the last instruction,
  * target record-full must be executed before
  */
(gdb) reverse-next

/** change the value of a varible
  * inside GDB when running the program
  */
(gdb) set var {varible name} = {some value}

/** when multiple processes are running (ex: fork), 
  * let GDB know which process to debug 
  */
(gdb) set follow-fork-mode [child | parent]
  
```

