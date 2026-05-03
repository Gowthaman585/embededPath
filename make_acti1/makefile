CC = gcc
all: my_program
my_program:	functions.o	main.o
	$(CC) functions.o main.o -o my_program
functions.o:	functions.c
	$(CC) -c functions.c -o functions.o
main.o:	main.c
	$(CC) -c main.c -o main.o
clean:
	rm -rf *.o my_program
	
