# TypeScript Compiler (TSC) Execution Flow

> **Goal:** Understand how the TypeScript compiler converts TypeScript into JavaScript while ensuring syntax correctness and type safety.

---

# Compiler Pipeline

```text
TypeScript Source Code
        │
        ▼
1. Lexer (Scanner)
        │
        ▼
2. Parser
        │
        ▼
3. AST (Abstract Syntax Tree)
        │
        ▼
4. Binder
        │
        ▼
5. Checker (Type Checker)
        │
        ▼
6. Emitter
        │
        ▼
JavaScript (.js)
Declaration Files (.d.ts)
Source Maps (.map)
```

---

# Compiler Phases Overview

| Phase | Purpose | Output |
|--------|----------|---------|
| Lexer | Converts characters into tokens | Token Stream |
| Parser | Validates syntax and builds AST | AST |
| Binder | Creates symbols and scopes | Symbol Table |
| Checker | Performs type checking and semantic analysis | Checked AST |
| Emitter | Generates JavaScript and other files | .js, .d.ts, .map |

---

# 1. Lexer (Scanner)

## Definition

The **Lexer** (also called the **Scanner**) is the first phase of the TypeScript compiler.

It reads the source code **character by character** and converts it into **tokens**, which are the smallest meaningful units of a programming language.

---

## Example

```ts
const age: number = 22;
```

Generated Tokens

```text
const
age
:
number
=
22
;
```

---

## Responsibilities

- Reads source code character by character
- Removes whitespace
- Ignores comments
- Converts text into tokens

---

## Input

```text
TypeScript Source Code
```

## Output

```text
Token Stream
```

---

## Why is the Lexer Needed?

The compiler cannot understand raw text directly.

Instead, it first converts the source code into tokens, making it easier for the parser to understand the structure of the program.

---

## Interview Question

### Q. What is a Token?

**Answer**

A token is the smallest meaningful unit of source code produced by the Lexer.

Examples:

```text
if
const
=
+
identifier
number
string
```

---

# 2. Parser

## Definition

The **Parser** reads the token stream and verifies whether the code follows TypeScript grammar.

If the syntax is correct, it builds an **Abstract Syntax Tree (AST).**

---

## Example

```ts
if (age > 18) {
    console.log(age);
}
```

Valid Syntax ✅

---

Invalid Example

```ts
if(age > ){
```

Parser Output

```text
Syntax Error
Unexpected Token
```

---

## Responsibilities

- Validates syntax
- Checks language grammar
- Creates the AST

---

## Input

```text
Token Stream
```

## Output

```text
Abstract Syntax Tree (AST)
```

---

## Important Point

The Parser **does NOT perform type checking.**

It only checks whether the syntax is valid.

---

## Interview Question

### Q. What happens if there is a syntax error?

Compilation stops at the Parser stage.

The Checker is **not executed**.

---

# 3. AST (Abstract Syntax Tree)

## Definition

An **Abstract Syntax Tree (AST)** is a tree representation of the source code.

Each statement, expression, declaration, or operator becomes a node.

---

## Example

```ts
const x = 10;
```

AST

```text
VariableDeclaration
├── Identifier (x)
└── NumericLiteral (10)
```

---

Another Example

```ts
a + b * c
```

AST

```text
        +
      /   \
     a     *
          / \
         b   c
```

The parser correctly applies **operator precedence**, so multiplication happens before addition.

---

## Responsibilities

- Represents program structure
- Maintains syntax hierarchy
- Used by later compiler phases

---

## Why AST?

The compiler performs all later operations (binding, type checking, code generation) using the AST instead of raw text.

---

# 4. Binder

## Definition

The **Binder** connects all AST nodes and creates relationships between declarations and references.

This is where TypeScript understands:

- Variables
- Functions
- Classes
- Interfaces
- Scopes
- Symbols

---

# What Does the Binder Create?

- Symbol Tables
- Parent Pointers
- Scope Information
- Flow Nodes

---

## Symbol Table

A Symbol Table maps identifiers to their declarations.

Example

```ts
let age = 22;

console.log(age);
```

Symbol Table

```text
age
 ↓
Variable Declaration
```

Now the compiler knows exactly which variable is being referenced.

---

## Parent Pointer

Each AST node stores its parent.

Example

```text
Function
   │
Variable
```

Variable Node

```text
parent → Function
```

Useful for navigating upward through the AST.

---

## Scope Creation

Example

```ts
let a = 10;

function demo() {
    let b = 20;
}
```

Scopes

```text
Global Scope
 └── a

Function Scope
 └── b
```

---

## Flow Nodes

Flow Nodes are used for **Control Flow Analysis**.

Example

```ts
if (age > 18) {
    console.log(age);
}
```

Flow Graph

```text
Start
   │
Condition
 /     \
True   False
```

---

## Responsibilities

- Creates Symbol Tables
- Creates Scopes
- Links identifiers with declarations
- Adds Parent Pointers
- Builds Flow Graphs

---

## Why is the Binder Needed?

Without the Binder, the compiler wouldn't know which declaration an identifier refers to.

---

## Interview Question

### Q. What is the role of the Binder?

**Answer**

The Binder creates symbol tables, scope information, parent pointers, and connects identifiers with their declarations.

---

# 5. Checker (Type Checker)

## Definition

The **Checker** performs **Semantic Analysis**.

It is the most intelligent phase of the compiler and is responsible for ensuring type safety.

---

# Responsibilities

- Type Checking
- Type Inference
- Generic Resolution
- Function Overload Resolution
- Control Flow Analysis
- Null Checking
- Compatibility Checking

---

# Type Checking

Example

```ts
let age: number = "22";
```

Error

```text
Type 'string' is not assignable to type 'number'
```

---

# Type Inference

Example

```ts
let age = 22;
```

Compiler infers

```text
number
```

---

# Generic Resolution

Example

```ts
function identity<T>(value: T) {
    return value;
}

identity("Hello");
```

Compiler resolves

```text
T = string
```

---

# Function Overload Resolution

Example

```ts
function add(a: number, b: number): number;
function add(a: string, b: string): string;
```

The compiler selects the correct overload based on the provided arguments.

---

# Control Flow Analysis

Example

```ts
let value: string | undefined;

if (value) {
    value.toUpperCase();
}
```

Inside the `if` block,

```text
value → string
```

The compiler automatically narrows the type.

---

# Null Checking

Example

```ts
let name: string = null;
```

With `strictNullChecks`

```text
Error
null is not assignable to string
```

---

# Compatibility Checking

Example

```ts
interface User {
    name: string;
}

const person = {
    name: "John",
    age: 25
};

const user: User = person;
```

Allowed because the required structure matches.

---

## Important Point

The Checker runs **only if the Parser successfully validates the syntax.**

---

## Interview Question

### Parser vs Checker

| Parser | Checker |
|----------|-----------|
| Checks syntax | Checks types |
| Builds AST | Performs semantic analysis |
| Detects grammar errors | Detects type errors |

---

# 6. Emitter

## Definition

The **Emitter** converts the checked AST into JavaScript.

It also generates declaration files and source maps.

---

# Generated Files

### JavaScript

```text
.js
```

### Declaration File

```text
.d.ts
```

### Source Map

```text
.map
```

---

## Example

Input

```ts
const age: number = 22;
```

Generated JavaScript

```js
const age = 22;
```

Notice

Type annotations are removed because JavaScript has no type system.

---

## Declaration File

Input

```ts
export function add(a: number, b: number): number;
```

Generated

```ts
export declare function add(a: number, b: number): number;
```

Used for:

- IntelliSense
- Type Checking
- Library Support

---

## Source Maps

Source Maps map JavaScript back to the original TypeScript source.

Useful while debugging in:

- Chrome DevTools
- VS Code

---

# Complete Compiler Flow

```text
TypeScript Source Code
        │
        ▼
Lexer (Scanner)
        │
        ▼
Token Stream
        │
        ▼
Parser
        │
        ▼
Abstract Syntax Tree (AST)
        │
        ▼
Binder
 ├── Symbol Tables
 ├── Scope Information
 ├── Parent Pointers
 └── Flow Nodes
        │
        ▼
Checker
 ├── Type Checking
 ├── Type Inference
 ├── Generic Resolution
 ├── Overload Resolution
 ├── Control Flow Analysis
 ├── Compatibility Checking
 └── Null Checking
        │
        ▼
Emitter
 ├── JavaScript (.js)
 ├── Declaration Files (.d.ts)
 └── Source Maps (.map)
```

---

# Parser vs Binder vs Checker

| Feature | Parser | Binder | Checker |
|----------|----------|----------|----------|
| Validates Syntax | ✅ | ❌ | ❌ |
| Builds AST | ✅ | ❌ | ❌ |
| Creates Symbol Tables | ❌ | ✅ | ❌ |
| Creates Scopes | ❌ | ✅ | ❌ |
| Links Identifiers | ❌ | ✅ | ❌ |
| Performs Type Checking | ❌ | ❌ | ✅ |
| Type Inference | ❌ | ❌ | ✅ |
| Generic Resolution | ❌ | ❌ | ✅ |

---

# Frequently Asked Interview Questions

## 1. What are the phases of the TypeScript compiler?

**Answer**

Lexer → Parser → AST → Binder → Checker → Emitter

---

## 2. What is a Token?

The smallest meaningful unit of source code produced by the Lexer.

---

## 3. What is an AST?

A tree representation of the program structure generated by the Parser.

---

## 4. What is the role of the Binder?

The Binder creates symbol tables, scopes, parent pointers, and links identifiers with their declarations.

---

## 5. What is semantic analysis?

Semantic analysis ensures that the program is meaningful by checking types, scopes, generics, overloads, compatibility, and control flow.

---

## 6. What is the difference between Syntax Errors and Type Errors?

| Syntax Error | Type Error |
|---------------|------------|
| Found by Parser | Found by Checker |
| Invalid grammar | Invalid types |

---

## 7. Why are TypeScript types removed in JavaScript?

Because JavaScript has no runtime type system. Types exist only during compilation.

---

## 8. What files does the Emitter generate?

- JavaScript (`.js`)
- Declaration Files (`.d.ts`)
- Source Maps (`.map`)

---

## 9. Which phase is responsible for type inference?

The **Checker**.

---

## 10. Which phase creates symbol tables?

The **Binder**.

---

# 30-Second Interview Answer

> "The TypeScript compiler works in six major phases: **Lexer, Parser, AST, Binder, Checker, and Emitter**. The Lexer converts source code into tokens. The Parser validates syntax and builds an Abstract Syntax Tree (AST). The Binder creates symbol tables, scopes, and links identifiers to their declarations. The Checker performs semantic analysis such as type checking, type inference, generic resolution, overload resolution, and control-flow analysis. Finally, the Emitter generates JavaScript, declaration files (`.d.ts`), and source maps (`.map`). This pipeline ensures TypeScript code is syntactically correct, type-safe, and transformed into executable JavaScript."

---

# Quick Revision (1 Minute)

```text
Lexer
↓
Converts code → Tokens

Parser
↓
Checks syntax → AST

Binder
↓
Creates Symbols + Scopes

Checker
↓
Type Checking
Type Inference
Generics
Control Flow
Null Checking

Emitter
↓
Generates
.js
.d.ts
.map
```

---

# Memory Trick

```text
L → P → A → B → C → E

Lexer
Parser
AST
Binder
Checker
Emitter
```

**Mnemonic:**

> **"Lazy Programmers Always Build Clean Engines."**