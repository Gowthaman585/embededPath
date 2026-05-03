### NEW REPO ONLY FOR EMBEDED SYSTEMS LEARNINGS  
C and gnu utilities  
### NOTES:  
The project file may contains hundreds of program files in it repo.  
so handling the huge set of program files and making executables out of it , may arise multiple challenges.   
**How can we make object file of c program?**  
using gcc utility we can use -c flag to only compile the file without linking it.  
example: gcc -c main.c -c main.o  
*A formal command like "gcc main.c -o main.o can automatically complie and link and turn into executable file*".  
**Making of "make" file:**
The "make" is a powerful another gnu utility which is actually an build system make top of gnu/gcc.  
The make system orchestrates the given activity (set of commands) one by one.  
Every repo contains a "makefile" or "Makefile" which is like a main.c form a project.  
The command "make" simply triggers the "makfile" activity one-by-one.  
*RULES:  
all: "target_filename_which_the_utlimate_aim_of_the_project  
other target file name (modules name): their_dependenties    
example make_file:  
CC(varibale name ) = gcc (utilite/compiler name)
objfile1: codeFile1.c
<tab> CC -c codeFile1.c -o codeFile1.o
objfile2: codeFile2.c
<tab> CC -c codeFile2.c -o codeFile2.o  
clean:  
<tab> rm -rf objfile1 objfile2 program_executables  
