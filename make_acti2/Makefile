include source.mk

PLATFORM = HOST

ifeq ($(PLATFORM) , HOST)
	CC = gcc
	CFLAGS= -Wall -o0 -g
else
	CC = arm-none-eabi-gcc
	CFLAGS = -mcpu=cortex-m4 -mthumb -Wall -O0 -g
endif

OBJ = $(SRC:.c=.o)

.PHONY = all clean

all : my_program

%.o : %.c
	$(CC) $(CFLAGS) -c $< -o $@

my_program : $(OBJ)
	$(CC) $(OBJ) -o my_program

clean:
	rm -f *.o my_program
