# 🛠️ Advanced Build Automation: Dynamic Suffix Replacement

This repository demonstrates how to implement dynamic suffix replacement inside a `Makefile` to automate multi-file compilation and linking pipelines without hardcoding individual files.

---

## 💡 Usage of `source.mk`

By utilizing a source tracking pattern, we completely overcome the tedious requirement of declaring each individual file for compiling and linking.

### The Old Way (Manual Targets)

Explicitly writing a target recipe for every single source file quickly leads to bloated, unmaintainable Makefiles:

```makefile
main.o : main.c
	$(CC) -c main.c -o main.o
```

### The Optimized Way (Dynamic Suffix Replacement)

Instead of manual declarations, we define a list of source files and use macro substitution to automatically generate object file requirements on the fly:

```makefile
OBJ = $(SRC:.c=.o)
```

---

## 📜 Makefile Execution & Linking

Here is the clean snippet demonstrating how to correctly bridge dynamic variables to link your final target binary executable:

```makefile
# Default overarching target
all : my_program

# The Linking Phase
my_program : $(OBJ)
	$(CC) $(OBJ) -o my_program
```
