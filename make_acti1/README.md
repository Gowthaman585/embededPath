# 🔧 Basic Multi-File C Compilation with Make

This activity demonstrates how to split a C program across multiple source files and wire them together using a `Makefile` with explicit targets.

---

## 📁 Project Structure

```
make_acti1/
├── main.c        # Entry point — calls add_numbers()
├── functions.c   # Implementation — defines add_numbers()
├── makefile      # Build instructions
└── my_program    # Compiled output binary
```

---

## 📄 Source Files

### `functions.c`
Defines a simple integer addition function:

```c
int add_numbers(int a, int b) {
    return a + b;
}
```

### `main.c`
Declares the function via a prototype, calls it, and prints the result:

```c
#include <stdio.h>

int add_numbers(int a, int b);

int main() {
    int result = add_numbers(5, 10);
    printf("result = %d\n", result);
    return 0;
}
```

---

## 🛠️ Makefile

```makefile
CC = gcc

all: my_program

my_program: functions.o main.o
	$(CC) functions.o main.o -o my_program

functions.o: functions.c
	$(CC) -c functions.c -o functions.o

main.o: main.c
	$(CC) -c main.c -o main.o

clean:
	rm -rf *.o my_program
```

### Build Targets

| Target | Description |
|--------|-------------|
| `all` | Default target — builds the final binary |
| `my_program` | Links `functions.o` and `main.o` into the executable |
| `functions.o` | Compiles `functions.c` into an object file |
| `main.o` | Compiles `main.c` into an object file |
| `clean` | Removes all object files and the binary |

---

## ▶️ Usage

```bash
# Build the program
make

# Run the binary
./my_program
# Output: result = 15

# Clean build artifacts
make clean
```

---

## 🔍 How It Works

1. `make` evaluates the `all` target, which depends on `my_program`
2. `my_program` depends on both `.o` object files, so Make compiles each source file first
3. Once both object files exist, GCC links them into the final executable `my_program`
4. Re-running `make` only recompiles files whose source has changed — Make tracks dependencies automatically
