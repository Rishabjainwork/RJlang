# RJLang 🚀

### A syntax-flexible programming language experiment

RJLang is an experimental programming language and compiler project built around a simple idea:

> **The programmer should not have to remember the exact syntax of a programming language to express what they mean.**

Different programming languages often provide different syntax for the same operation.

For example, getting the length of a collection may look like:

```cpp
nums.size()
```

in C++, while another language may use:

```java
nums.length
```

and another may use:

```python
len(nums)
```

RJLang aims to make all of these valid ways of expressing the **same operation**.

```text
nums.size()
nums.length
len(nums)
length(nums)
```

All of them should eventually mean:

```text
LENGTH(nums)
```

The goal is to create a programming environment where syntax can be mixed freely while the compiler focuses on understanding the programmer's intended operation.

---

## 🎯 The Core Idea

Traditional programming languages are strict about syntax.

If you are writing Python, you need to remember Python's syntax.

If you are writing C++, you need to remember C++ syntax.

If you are writing Java, you need to remember Java syntax.

RJLang explores a different approach:

```text
                 Programmer Code
                       │
                       ▼
              ┌─────────────────┐
              │ Understand Code │
              └────────┬────────┘
                       │
                       ▼
                Common Meaning
                       │
                       ▼
              ┌─────────────────┐
              │ Generate Code   │
              └────────┬────────┘
                       │
                       ▼
                 Executable Code
```

The syntax becomes a way of expressing an operation rather than a rigid rule that must be memorized perfectly.

---

# 💡 Example

Eventually, RJLang should allow code such as:

```text
nums = [10, 20, 30, 40, 50]

print(nums.size())
print(nums.length)
print(len(nums))
print(length(nums))
```

All four statements should produce:

```text
5
5
5
5
```

The programmer used four different syntaxes, but RJLang understands that all four are asking for the same thing:

```text
GET THE LENGTH OF nums
```

---

# 🌎 Mixing Languages

The long-term vision is to allow syntax from multiple programming languages to exist in the same program.

For example:

```text
nums = [1, 2, 3, 4, 5]

print(nums.length)

for x in nums:
    System.out.println(x)

cout << len(nums)
```

This intentionally mixes:

- Python-style syntax
- Java-style syntax
- C++-style syntax
- RJLang's own syntax

Instead of treating the differences as errors, RJLang should normalize them into a common representation.

---

# 🧠 The Important Concept: Common Meaning

RJLang should not simply replace text.

For example:

```text
nums.size()
nums.length
len(nums)
length(nums)
```

should all become one internal operation:

```text
LENGTH(nums)
```

Similarly, different printing syntaxes could eventually become:

```text
PRINT("Hello")
```

For example:

```text
print("Hello")
cout << "Hello";
System.out.println("Hello");
console.log("Hello");
```

could all represent:

```text
PRINT("Hello")
```

This common representation is the foundation of the project.

---

# 🏗️ Compiler Architecture

The initial prototype is intentionally simple.

As the project develops, the architecture will move toward:

```text
                    RJLang Source
                         │
                         ▼
                    ┌─────────┐
                    │  Lexer  │
                    └────┬────┘
                         │
                         ▼
                    ┌─────────┐
                    │ Parser  │
                    └────┬────┘
                         │
                         ▼
                  ┌──────────────┐
                  │     AST      │
                  │ Common Model │
                  └──────┬───────┘
                         │
                         ▼
                Semantic Analysis
                         │
                         ▼
                  Code Generator
                         │
                         ▼
                    C++ / Other
                         │
                         ▼
                    Native Code
```

The most important part is the common representation.

For example:

```text
C++ syntax      ──┐
Java syntax     ──┤
Python syntax   ──┼──→ LENGTH(nums)
RJLang syntax   ──┘
```

This allows multiple syntaxes to represent the same operation.

---

# 🛠️ Development Roadmap

RJLang will be built incrementally.

## Phase 1 — Prototype

Create a tiny compiler capable of reading `.rj` files and generating C++.

Example:

```text
print("Hello World")
```

becomes:

```cpp
cout << "Hello World" << endl;
```

---

## Phase 2 — Syntax Aliases

Support multiple ways of performing the same operation.

### Length

```text
nums.size()
nums.length
len(nums)
length(nums)
```

→

```text
LENGTH(nums)
```

### Print

```text
print("Hello")
cout << "Hello";
System.out.println("Hello");
console.log("Hello");
```

→

```text
PRINT("Hello")
```

---

## Phase 3 — Variables

Support different declaration styles.

For example:

```cpp
int x = 10;
```

```python
x = 10
```

```java
var x = 10;
```

```javascript
let x = 10;
```

These could eventually map to:

```text
DECLARE x = 10
```

---

## Phase 4 — Expressions

Support multiple ways of expressing common operations.

For example:

```text
x + y
add(x, y)
x.add(y)
```

could represent:

```text
ADD(x, y)
```

The same idea can later be applied to:

- subtraction
- multiplication
- division
- comparison
- equality
- logical operations
- sorting
- searching
- collection operations

---

## Phase 5 — Control Flow

Support different styles of:

```text
if
else
for
while
```

For example:

### Python-style

```python
if x > 10:
    print(x)
```

### C++-style

```cpp
if (x > 10) {
    cout << x;
}
```

Both could represent the same internal structure.

---

## Phase 6 — Functions

Support different function syntaxes.

For example:

```python
def add(a, b):
    return a + b
```

and:

```cpp
int add(int a, int b) {
    return a + b;
}
```

could represent the same function internally.

---

## Phase 7 — Multiple Backends

The initial compiler will target C++.

Eventually, RJLang could generate:

```text
RJLang
   │
   ├──→ C++
   ├──→ Python
   ├──→ Java
   ├──→ JavaScript
   └──→ WebAssembly
```

The common representation makes this possible.

---

# 🔥 Why This Is Difficult

Making syntax aliases is relatively easy.

The difficult part is understanding **semantics**.

Programming languages differ in:

- Type systems
- Memory management
- Data structures
- Object models
- Function behavior
- Operators
- Scope rules
- Error handling
- Standard libraries
- Runtime behavior

For example:

```cpp
nums.size()
```

does not necessarily have exactly the same semantics as:

```java
nums.length
```

and:

```python
len(nums)
```

RJLang therefore cannot simply perform text replacement forever.

It will eventually need to understand:

> **What is `nums`?**

> **What operation is being requested?**

> **What does that operation mean?**

This is where compiler concepts such as ASTs, semantic analysis, type systems, and intermediate representations become important.

---

# 📁 Project Structure

The project currently starts very small:

```text
RJLang/
│
├── main.cpp
├── hello.rj
└── README.md
```

As the compiler grows, the structure can evolve into:

```text
RJLang/
│
├── src/
│   ├── lexer.cpp
│   ├── parser.cpp
│   ├── ast.cpp
│   ├── semantic.cpp
│   └── codegen.cpp
│
├── include/
│   ├── lexer.h
│   ├── parser.h
│   └── ast.h
│
├── examples/
│   ├── hello.rj
│   ├── arrays.rj
│   └── functions.rj
│
├── tests/
│
├── README.md
└── main.cpp
```

---

# ▶️ Running the Current Prototype

The current prototype is a C++ program that acts as the RJLang compiler.

Compile it:

```bash
g++ main.cpp -o rjlang
```

Then compile an RJLang file:

```bash
./rjlang hello.rj
```

This generates:

```text
generated.cpp
```

Compile the generated C++:

```bash
g++ generated.cpp -o program
```

Run it:

```bash
./program
```

The current prototype demonstrates the basic pipeline:

```text
hello.rj
   ↓
RJLang Compiler
   ↓
generated.cpp
   ↓
C++ Compiler
   ↓
program
```

---

# 🧪 Example of the Desired Future

A future RJLang program might look like:

```text
nums = [10, 20, 30, 40, 50]

print(nums.size())

for x in nums:
    System.out.println(x)

if nums.length > 3:
    cout << "Large array"

print(len(nums))
```

RJLang would interpret the different syntaxes and normalize them into a common representation such as:

```text
DECLARE nums = ARRAY(10, 20, 30, 40, 50)

PRINT(LENGTH(nums))

FOR x IN nums:
    PRINT(x)

IF LENGTH(nums) > 3:
    PRINT("Large array")

PRINT(LENGTH(nums))
```

The final output could then be generated in C++ or another supported target.

---

# 📚 What This Project Teaches

Building RJLang provides hands-on experience with:

- C++
- Compiler design
- Programming language design
- Lexical analysis
- Parsing
- Abstract Syntax Trees
- Intermediate representations
- Semantic analysis
- Type systems
- Code generation
- Language interoperability
- Static analysis
- Error handling

Instead of only learning compiler theory, the goal is to implement each concept as the project grows.

---

# 🚧 Current Status

**Status:** Early prototype

Currently, RJLang can:

- Read a `.rj` source file
- Recognize a small amount of custom syntax
- Generate C++ code
- Use the normal C++ compiler to create an executable

The immediate next goal is to implement the first real syntax-independent operation:

```text
nums.size()
nums.length
len(nums)
length(nums)
```

All should resolve to:

```text
LENGTH(nums)
```

---

# 🗺️ Long-Term Vision

The ultimate vision of RJLang is:

```text
       Python syntax ────┐
       Java syntax ──────┤
       C++ syntax ───────┤
       JavaScript syntax ┤
       RJLang syntax ────┤
                         ▼
                  ┌─────────────┐
                  │   RJLang    │
                  │   Compiler  │
                  └──────┬──────┘
                         │
                   Common Meaning
                         │
             ┌───────────┼───────────┐
             ▼           ▼           ▼
            C++        Python       Java
```

The goal is not to make programmers memorize another complicated syntax.

The goal is to explore whether a programming language can be **flexible about syntax while remaining precise about meaning**.

---

# 💭 Philosophy

Traditional programming:

> **"Learn the syntax, then tell the computer what to do."**

RJLang explores:

> **"Tell the computer what you mean, and let the compiler handle the syntax."**

RJLang is an experiment to see how far this idea can be taken.

---

# 👨‍💻 Author

**Rishab Jain**

RJLang is an experimental project for learning and exploring:

- Programming languages
- Compiler construction
- C++
- Syntax normalization
- Semantic representations
- Code generation

---

# ⭐ Project Goal

Build a programming language where this:

```text
nums.size()
```

this:

```text
nums.length
```

this:

```text
len(nums)
```

and this:

```text
length(nums)
```

can all mean:

```text
LENGTH(nums)
```

**Because the programmer knows what they want to do — they just shouldn't have to remember which language calls it what.**
