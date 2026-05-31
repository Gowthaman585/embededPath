# 🔧 Embedded Systems Learning — C & GNU Utilities

> A structured repository for learning embedded systems programming in C, covering compilation workflows, GNU toolchain utilities, and build system automation with `make`.

---

## 📁 Repository Structure

This repository may contain **hundreds of program files** organized as modular C projects. Each module is compiled independently into object files, then linked into a final executable — a workflow that mirrors real embedded systems development.

---

## ⚙️ Compilation with GCC

### Object File Compilation (`-c` flag)

To compile a C source file **without linking** (producing a `.o` object file):

```bash
gcc -c main.c -o main.o
```

| Flag | Purpose |
|------|---------|
| `-c` | Compile only — skip the linker |
| `-o` | Specify the output filename |

### Full Compilation + Linking

To compile **and** link in one step, producing an executable:

```bash
gcc main.c -o main
```

> ⚠️ **Key distinction:** Using `-c` stops at the object file stage. Omitting `-c` compiles, links, and produces a runnable executable.

---

## 🛠️ The `make` Build System

### What is `make`?

`make` is a powerful **GNU build automation utility** built on top of GCC. It reads a `Makefile` (the project's build blueprint) and orchestrates compilation commands **sequentially and intelligently** — only rebuilding files that have changed.

Think of `Makefile` as the `main.c` of your build system: the single entry point that ties everything together.

### Running `make`

```bash
make          # Executes the default (first) target
make clean    # Runs the 'clean' target to remove build artifacts
```

---

## 📄 Makefile Structure & Rules

### Anatomy of a Rule

```makefile
target: dependencies
	command
```

| Component | Description |
|-----------|-------------|
| `target` | The file to be produced (or a phony action like `clean`) |
| `dependencies` | Files this target depends on — if they change, the target rebuilds |
| `command` | Shell command to execute (must be indented with a **tab**, not spaces) |

### The `all` Target

The `all` target defines the **ultimate goal** of the build — typically the final executable. It should list all required modules as dependencies:

```makefile
all: program_executable
```

---

## 📝 Example Makefile

```makefile
# Compiler variable — easy to swap out (e.g., arm-none-eabi-gcc for embedded targets)
CC = gcc

# Default target — builds the final executable
all: program_executable

# Compile module 1
codeFile1.o: codeFile1.c
	$(CC) -c codeFile1.c -o codeFile1.o

# Compile module 2
codeFile2.o: codeFile2.c
	$(CC) -c codeFile2.c -o codeFile2.o

# Link all object files into the final executable
program_executable: codeFile1.o codeFile2.o
	$(CC) codeFile1.o codeFile2.o -o program_executable

# Remove all build artifacts
clean:
	rm -rf codeFile1.o codeFile2.o program_executable
```

### How It Works

```
codeFile1.c ──┐
               ├──[gcc -c]──► codeFile1.o ──┐
codeFile2.c ──┘                              ├──[gcc link]──► program_executable
                              codeFile2.o ──┘
```

---

## 🧹 The `clean` Target

The `clean` target removes all compiled artifacts to allow a fresh build:

```makefile
clean:
	rm -rf codeFile1.o codeFile2.o program_executable
```

Run it with:

```bash
make clean
```

> 💡 `clean` is a **phony target** — it doesn't produce a file named `clean`. For safety in larger projects, declare it explicitly:
> ```makefile
> .PHONY: clean all
> ```

---

## 🚀 Quick Reference

| Task | Command |
|------|---------|
| Compile to object file | `gcc -c file.c -o file.o` |
| Compile & link to executable | `gcc file.c -o program` |
| Run the build | `make` |
| Clean build artifacts | `make clean` |
| Build a specific target | `make target_name` |

---

## 📚 Prerequisites

- **GCC** — GNU Compiler Collection
- **GNU Make** — Build automation tool
- A Linux/Unix environment or WSL on Windows

---

*Part of an embedded systems learning series — C fundamentals, GNU toolchain, and bare-metal programming.*
