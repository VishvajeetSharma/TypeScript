# Module 2 — Type System

> **Difficulty:** Beginner  
> **Interview Importance:** ⭐⭐⭐⭐⭐  
> **Prerequisite:** Module 1 — Introduction to TypeScript

---

# What is a Type System?

A **Type System** is a set of rules that defines what kind of values can be stored in variables, passed to functions, or returned from functions.

The TypeScript type system helps developers:

- Detect errors during compilation
- Improve code readability
- Prevent invalid operations
- Enable better IDE support
- Make applications safer and easier to maintain

Unlike JavaScript, TypeScript checks types **before the code runs**.

---

# Why Do We Need Types?

Consider this JavaScript code:

```javascript
let age = 20;

age = "Twenty";
```

JavaScript allows this.

But imagine later:

```javascript
console.log(age + 10);
```

Output:

```
Twenty10
```

This may not be the intended behavior.

With TypeScript:

```typescript
let age: number = 20;

age = "Twenty";
```

Compilation Error:

```
Type 'string' is not assignable to type 'number'.
```

TypeScript catches the mistake before execution.

---

# Categories of Types

TypeScript types can be broadly categorized into:

```
TypeScript Types

│

├── Primitive Types
│     ├── string
│     ├── number
│     ├── boolean
│     ├── bigint
│     ├── symbol
│     ├── null
│     └── undefined
│
├── Special Types
│     ├── any
│     ├── unknown
│     ├── never
│     └── void
│
└── Advanced Types
      ├── Array
      ├── Tuple
      ├── Union
      ├── Interface
      ├── Generics
      └── ...
```

This module focuses on **Primitive Types** and **Special Types**.

---

# Primitive Types

Primitive types represent single immutable values.

## 1. string

Represents textual data.

```typescript
let firstName: string = "Rahul";

console.log(firstName);
```

Examples:

```typescript
let city: string = "Delhi";
let language: string = "TypeScript";
```

---

### Common String Methods

```typescript
let message: string = "Hello";

message.length;

message.toUpperCase();

message.toLowerCase();

message.includes("He");
```

---

### Interview Question

**Q:** Can string store numbers?

Yes, but as text.

```typescript
let value: string = "100";
```

This is different from:

```typescript
let value: number = 100;
```

---

# 2. number

Represents all numeric values.

Unlike many languages, TypeScript has only one number type.

It includes:

- Integers
- Floating-point numbers
- Negative numbers
- Infinity
- NaN

Example:

```typescript
let age: number = 25;

let price: number = 99.99;

let marks: number = 95;
```

---

### Operations

```typescript
let x: number = 20;

let y: number = 10;

console.log(x + y);

console.log(x - y);

console.log(x * y);

console.log(x / y);
```

---

# 3. boolean

Represents logical values.

Possible values:

- true
- false

Example:

```typescript
let isLoggedIn: boolean = true;

let isAdmin: boolean = false;
```

---

### Common Usage

```typescript
if (isLoggedIn) {
    console.log("Welcome");
}
```

---

# 4. bigint

Represents integers larger than `Number.MAX_SAFE_INTEGER`.

Example:

```typescript
let hugeNumber: bigint = 123456789012345678901234567890n;
```

Notice the `n` suffix.

---

### Why BigInt?

JavaScript numbers lose precision for very large integers.

```typescript
let large = 999999999999999999999;
```

May lose precision.

Instead:

```typescript
let large = 999999999999999999999n;
```

---

### BigInt Operations

```typescript
let a = 100n;

let b = 50n;

console.log(a + b);
```

Cannot mix `number` and `bigint`.

Incorrect:

```typescript
10n + 5;
```

Compilation Error.

---

# 5. symbol

Represents a unique and immutable identifier.

```typescript
let id = Symbol();

let anotherId = Symbol();
```

Comparison:

```typescript
console.log(id === anotherId);
```

Output:

```
false
```

Every Symbol is unique.

---

### Real-world Usage

- Object property keys
- Private identifiers
- Library internals
- Meta programming

---

# 6. null

Represents the intentional absence of a value.

```typescript
let data: null = null;
```

Example:

```typescript
let selectedUser = null;
```

Meaning:

"No user is currently selected."

---

# 7. undefined

Represents a variable that has been declared but not assigned.

```typescript
let username: undefined = undefined;
```

Example:

```typescript
let age;

console.log(age);
```

Output:

```
undefined
```

---

# Special Types

Special types provide additional flexibility and control in the type system.

---

# 1. any

`any` disables TypeScript's type checking.

Example:

```typescript
let value: any = 10;

value = "Hello";

value = true;

value = {};

value = [];
```

Everything is allowed.

---

### Dangerous Example

```typescript
let user: any = "Rahul";

user.toFixed();
```

No compile-time error.

Runtime Error:

```
toFixed is not a function
```

---

### When to Use any

Only when absolutely necessary.

Examples:

- Migrating JavaScript to TypeScript
- Third-party libraries without type definitions
- Temporary development

Avoid using `any` in production code whenever possible.

---

# 2. unknown

`unknown` is the safer version of `any`.

You can store any value, but you **cannot use it until its type is checked**.

Example:

```typescript
let value: unknown;

value = 10;

value = "Hello";

value = true;
```

Accessing methods directly is not allowed:

```typescript
value.toUpperCase();
```

Compilation Error.

---

### Correct Usage

```typescript
if (typeof value === "string") {
    console.log(value.toUpperCase());
}
```

---

### Why unknown?

It forces developers to perform type checks before using values, improving safety.

---

# 3. void

Represents the absence of a return value.

Mostly used for functions.

Example:

```typescript
function printMessage(): void {
    console.log("Hello");
}
```

This function returns nothing.

---

### Incorrect

```typescript
function demo(): void {
    return 10;
}
```

Compilation Error.

---

# 4. never

Represents values that **never occur**.

A function returning `never` never completes normally.

Example:

```typescript
function throwError(): never {
    throw new Error("Something went wrong");
}
```

Another example:

```typescript
function infiniteLoop(): never {
    while (true) {}
}
```

---

### When is never used?

- Functions that throw errors
- Infinite loops
- Exhaustive type checking in switch statements

---

# Type Comparison

## any vs unknown

| Feature | any | unknown |
|----------|-----|----------|
| Accepts any value | ✅ | ✅ |
| Type checking | ❌ Disabled | ✅ Required before use |
| Safe | ❌ | ✅ |
| Can call methods directly | ✅ | ❌ |
| Recommended | Rarely | Yes |

### Example

```typescript
let value: any = "Hello";

value.toUpperCase();
```

Allowed.

---

```typescript
let value: unknown = "Hello";

value.toUpperCase();
```

Compilation Error.

Correct:

```typescript
if (typeof value === "string") {
    value.toUpperCase();
}
```

---

## void vs never

| Feature | void | never |
|----------|------|--------|
| Returns normally | ✅ | ❌ |
| Used for normal functions | ✅ | ❌ |
| Throws error | ❌ | ✅ |
| Infinite loop | ❌ | ✅ |

### void Example

```typescript
function greet(): void {
    console.log("Hello");
}
```

---

### never Example

```typescript
function fail(): never {
    throw new Error();
}
```

---

## null vs undefined

| null | undefined |
|------|------------|
| Intentional absence of value | Variable not initialized |
| Assigned manually | Usually assigned automatically |
| Type is null | Type is undefined |

Example:

```typescript
let user = null;
```

Meaning:

"No user exists."

---

```typescript
let age;

console.log(age);
```

Output:

```
undefined
```

Meaning:

"No value has been assigned."

---

# Type Inference

TypeScript can infer types automatically.

```typescript
let city = "Delhi";
```

Type inferred:

```typescript
string
```

Another example:

```typescript
let price = 200;
```

Type inferred:

```typescript
number
```

---

# Practice

## Create Variables Using Every Type

```typescript
// string
let name: string = "Rahul";

// number
let age: number = 22;

// boolean
let isStudent: boolean = true;

// bigint
let population: bigint = 1400000000n;

// symbol
let id: symbol = Symbol("id");

// null
let emptyValue: null = null;

// undefined
let notAssigned: undefined = undefined;

// any
let anything: any = "Hello";
anything = 100;
anything = true;

// unknown
let unknownValue: unknown = "TypeScript";

// void
function print(): void {
    console.log("Printing...");
}

// never
function crash(): never {
    throw new Error("Application Crashed");
}
```

---

# Real-World Examples

### API Response

```typescript
let response: unknown = fetchData();
```

Check before use:

```typescript
if (typeof response === "string") {
    console.log(response.toUpperCase());
}
```

---

### User Login

```typescript
let isLoggedIn: boolean = true;
```

---

### Product Price

```typescript
let price: number = 599.99;
```

---

### User Name

```typescript
let username: string = "Aman";
```

---

### Error Function

```typescript
function unauthorized(): never {
    throw new Error("Unauthorized");
}
```

---

# Common Interview Questions

## Q1. What is the difference between `any` and `unknown`?

**Answer:**  
Both can hold any value, but `any` disables all type checking, whereas `unknown` requires type narrowing before the value can be used. `unknown` is safer and preferred.

---

## Q2. What is the difference between `void` and `never`?

**Answer:**  
`void` indicates that a function completes without returning a value. `never` indicates that a function never completes normally, such as one that always throws an error or runs forever.

---

## Q3. What is the difference between `null` and `undefined`?

**Answer:**  
`null` is an explicitly assigned value representing "no value," while `undefined` typically means a variable has been declared but not initialized.

---

## Q4. Why should we avoid `any`?

**Answer:**  
`any` disables TypeScript's type checking, allowing invalid operations that may cause runtime errors. Overusing it defeats the purpose of TypeScript.

---

## Q5. When should `unknown` be used?

**Answer:**  
Use `unknown` when the type of a value is not known in advance (e.g., API responses or user input). Narrow the type before using it.

---

## Q6. Can we mix `number` and `bigint`?

**Answer:**  
No. TypeScript does not allow arithmetic operations between `number` and `bigint`. Explicit conversion is required.

---

# Best Practices

- Prefer specific types over `any`.
- Use `unknown` instead of `any` whenever possible.
- Enable `strictNullChecks` in `tsconfig.json`.
- Let TypeScript infer types when they are obvious.
- Use `void` only for functions that intentionally return nothing.
- Use `never` only for impossible code paths, infinite loops, or functions that always throw.

---

# Common Mistakes

- Using `any` everywhere.
- Confusing `void` with `never`.
- Assuming `null` and `undefined` are identical.
- Calling methods on `unknown` without type narrowing.
- Mixing `number` and `bigint` in arithmetic operations.

---

# Summary

- Primitive types represent basic values such as `string`, `number`, `boolean`, `bigint`, `symbol`, `null`, and `undefined`.
- Special types (`any`, `unknown`, `void`, `never`) provide additional flexibility and control.
- `unknown` is a safer alternative to `any`.
- `void` means "no return value"; `never` means "no normal completion."
- Understanding these types is essential for writing safe, maintainable TypeScript code.

---

# Cheat Sheet

| Type | Purpose |
|------|---------|
| `string` | Text values |
| `number` | Numeric values |
| `boolean` | `true` / `false` |
| `bigint` | Very large integers |
| `symbol` | Unique identifiers |
| `null` | Intentional absence of a value |
| `undefined` | Variable declared but not assigned |
| `any` | Disables type checking (avoid) |
| `unknown` | Safer alternative to `any` |
| `void` | Function returns nothing |
| `never` | Function never returns |

### Quick Revision

- `any` → Unsafe, disables type checking.
- `unknown` → Safe, requires type checks.
- `void` → No return value.
- `never` → Never returns.
- `null` → Explicitly empty.
- `undefined` → Not initialized.
- Prefer `unknown` over `any`.
- Use `strictNullChecks` for better null safety.