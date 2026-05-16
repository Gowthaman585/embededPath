## SECOND ACTIVITY

Usage of source.mk:  
by utilizing the source.mk we can overcome the need of  
declaring each individual file for compiling them into  
executable or linking.  
  
<!--
How to create a source.mk file
steps:
touch source.mk
< open > source.mk
SRC = main.c func.c proc.c etc..  
-->
    
for example:  
main.o : main.c  
    $(CC) -c main.c -o main.o  
instead:  
    OBJ = $(SRC:.c=.o)
<!--
The source.mk file include all the program source file
like main.c,fun1.c 
example: SRC = fun.c main.c proc.c etc...  
this statement access the included file in source.mk
one by one and then compile them into object file.  
-->

How to implement linking them into final executables?  
example makefile snippet:  
all : my_program  
my_program : $(OBJ)
    $(CC) $(OBJ) -o my_program  
<!--
the $(OBJ) consists of all necessary object files compiler  
by the previous declarations.  
The abstracted excution of this command is   
gcc main.o func.o proc.o -o my_program (linking the obj into executbales)  
-->

