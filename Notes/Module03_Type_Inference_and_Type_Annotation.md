# Module 3 — Type Inference & Type Annotation

> **Difficulty:** Beginner  
> **Interview Importance:** ⭐⭐⭐⭐⭐  
> **Prerequisite:** Module 2 — Type System

---

# What is Type Inference?

**Type Inference** is TypeScript's ability to **automatically determine the type of a variable, function return value, or expression without explicitly specifying it**.

In simple words:

> **TypeScript "guesses" the type based on the value assigned.**

Example:

```typescript
let name = "John";
```

Although no type is written, TypeScript automatically infers:

```typescript
let name: string;
```

Similarly,

```typescript
let age = 20;
```

becomes

```typescript
let age: number;
```

---

# Why Do We Need Type Inference?

Without type inference, we would need to specify the type of every variable.

Example:

```typescript
let firstName: string = "Rahul";
let age: number = 22;
let isStudent: boolean = true;
```

This works, but it becomes repetitive.

With type inference:

```typescript
let firstName = "Rahul";
let age = 22;
let isStudent = true;
```

The result is exactly the same, but the code is cleaner and easier to read.

---

# How Type Inference Works

TypeScript analyzes the assigned value and determines its type automatically.

```typescript
let city = "Delhi";
```

TypeScript infers:

```typescript
string
```

---

```typescript
let marks = 95;
```

Type:

```typescript
number
```

---

```typescript
let isLoggedIn = false;
```

Type:

```typescript
boolean
```

---

```typescript
let colors = ["Red", "Green", "Blue"];
```

Type:

```typescript
string[]
```

---

```typescript
let scores = [10, 20, 30];
```

Type:

```typescript
number[]
```

---

```typescript
let user = {
    id: 1,
    name: "Rahul"
};
```

Type inferred:

```typescript
{
    id: number;
    name: string;
}
```

---

# Type Inference Examples

## Example 1

```typescript
let language = "TypeScript";
```

Inferred Type:

```typescript
string
```

---

## Example 2

```typescript
let price = 599.99;
```

Inferred Type:

```typescript
number
```

---

## Example 3

```typescript
let available = true;
```

Inferred Type:

```typescript
boolean
```

---

## Example 4

```typescript
const PI = 3.14;
```

Inferred Type:

```typescript
3.14
```

Notice:

For `const`, TypeScript often infers the **literal type** instead of the broader primitive type.

---

# What is Type Annotation?

**Type Annotation** means **explicitly telling TypeScript what the type should be.**

Syntax:

```typescript
variableName: Type
```

Example:

```typescript
let age: number = 20;
```

Here,

```typescript
:number
```

is the type annotation.

---

Another example:

```typescript
let username: string = "John";
```

---

Boolean example:

```typescript
let isAdmin: boolean = false;
```

---

Array example:

```typescript
let marks: number[] = [90, 80, 70];
```

---

# Type Annotation vs Type Inference

## Type Annotation

You specify the type.

```typescript
let age: number = 20;
```

---

## Type Inference

TypeScript determines the type.

```typescript
let age = 20;
```

---

Both produce the same final type:

```typescript
number
```

---

# Why Use Type Annotation?

Although TypeScript can infer many types, explicit annotations improve readability and prevent unintended type inference in many scenarios.

Advantages:

- Makes code self-documenting
- Improves readability
- Prevents accidental type changes
- Useful for function parameters
- Recommended for public APIs

---

# When Should We Use Type Inference?

Use type inference when:

- The assigned value clearly indicates the type.
- The type is obvious.
- Local variables are initialized immediately.
- The code remains readable.

Example:

```typescript
let city = "Mumbai";

let count = 100;

let active = true;
```

No annotation is needed.

---

# When Should We Use Type Annotation?

Use type annotations for:

- Function parameters
- Function return types (especially exported functions)
- Variables declared without an initial value
- Complex objects
- Public APIs
- Class properties

Example:

```typescript
let username: string;
```

Without annotation:

```typescript
let username;
```

TypeScript infers:

```typescript
any
```

(when `noImplicitAny` is disabled)

Using an explicit type avoids ambiguity.

---

# Type Inference in Functions

## Parameter Types

TypeScript **does not infer parameter types** from nowhere.

Incorrect:

```typescript
function greet(name) {
    return "Hello " + name;
}
```

With `noImplicitAny` enabled, this produces an error because `name` has an implicit `any` type.

Correct:

```typescript
function greet(name: string) {
    return "Hello " + name;
}
```

---

## Return Type Inference

TypeScript can infer return types.

```typescript
function add(a: number, b: number) {
    return a + b;
}
```

Return type inferred:

```typescript
number
```

Equivalent explicit version:

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

---

# Type Inference with Arrays

Example:

```typescript
let fruits = ["Apple", "Banana", "Orange"];
```

Type inferred:

```typescript
string[]
```

---

Mixed values:

```typescript
let values = [10, "Hello"];
```

Type inferred:

```typescript
(string | number)[]
```

This is called a **Union Type**, which you'll learn in a later module.

---

# Type Inference with Objects

```typescript
let employee = {
    id: 101,
    name: "Aman",
    salary: 50000
};
```

Type inferred:

```typescript
{
    id: number;
    name: string;
    salary: number;
}
```

---

# Type Widening

Sometimes TypeScript infers a broader type than the exact value.

Example:

```typescript
let color = "Red";
```

Type:

```typescript
string
```

Even though the value is `"Red"`, `let` variables can change later.

---

For `const`:

```typescript
const color = "Red";
```

Type:

```typescript
"Red"
```

This is a **Literal Type** because `const` values cannot be reassigned.

---

# Type Narrowing (Introduction)

TypeScript can narrow types based on runtime checks.

Example:

```typescript
let value: string | number = "Hello";

if (typeof value === "string") {
    console.log(value.toUpperCase());
}
```

Inside the `if` block, TypeScript knows that `value` is a `string`.

---

# Real-World Examples

## User Name

```typescript
let username = "Rahul";
```

Type inferred:

```typescript
string
```

---

## Product Price

```typescript
let price: number = 999;
```

Explicit annotation.

---

## API Base URL

```typescript
const API_URL = "https://api.example.com";
```

Type inferred:

```typescript
"https://api.example.com"
```

---

## Shopping Cart

```typescript
let cartItems = ["Shoes", "Watch"];
```

Type inferred:

```typescript
string[]
```

---

## Function

```typescript
function multiply(a: number, b: number): number {
    return a * b;
}
```

Parameters are explicitly annotated, and the return type is explicitly declared.

---

# Best Practices

## ✅ Prefer Type Inference for Local Variables

```typescript
let total = 100;
```

Cleaner and easier to read.

---

## ✅ Use Type Annotation for Function Parameters

```typescript
function greet(name: string) {
    console.log(name);
}
```

---

## ✅ Explicitly Specify Return Types for Public Functions

```typescript
function getUserName(): string {
    return "Rahul";
}
```

This makes APIs easier to understand and protects against accidental changes.

---

## ✅ Annotate Variables Without Initial Values

```typescript
let email: string;

email = "user@example.com";
```

---

## ✅ Let TypeScript Do the Work

Avoid unnecessary annotations.

Instead of:

```typescript
let age: number = 20;
```

You can simply write:

```typescript
let age = 20;
```

unless the annotation adds clarity.

---

# Common Mistakes

## Mistake 1

Writing unnecessary annotations everywhere.

```typescript
let city: string = "Delhi";
```

When this is sufficient:

```typescript
let city = "Delhi";
```

---

## Mistake 2

Leaving variables untyped.

```typescript
let user;
```

Avoid this.

Better:

```typescript
let user: string;
```

---

## Mistake 3

Not annotating function parameters.

```typescript
function print(value) {}
```

Correct:

```typescript
function print(value: string) {}
```

---

## Mistake 4

Assuming TypeScript infers everything.

It infers many types, but **not all**, especially function parameters and complex generic scenarios.

---

# Practice

## Practice 1 — Infer Types

Determine the inferred type of each variable.

```typescript
let name = "John";

let age = 20;

let isAdmin = false;

let salary = 55000.50;

let cities = ["Delhi", "Mumbai"];

let numbers = [10, 20, 30];

let employee = {
    id: 1,
    name: "Rahul"
};
```

**Expected Types:**

- `name` → `string`
- `age` → `number`
- `isAdmin` → `boolean`
- `salary` → `number`
- `cities` → `string[]`
- `numbers` → `number[]`
- `employee` → `{ id: number; name: string }`

---

## Practice 2 — Explicit Annotations

Add the correct type annotation.

```typescript
let name: string = "John";

let age: number = 20;

let isAdmin: boolean = false;

let marks: number[] = [90, 80, 70];

let country: string = "India";
```

---

## Practice 3 — Functions

Write appropriate parameter and return types.

```typescript
function add(a: number, b: number): number {
    return a + b;
}

function print(message: string): void {
    console.log(message);
}
```

---

# Common Interview Questions

## Q1. What is Type Inference?

**Answer:**  
Type Inference is TypeScript's ability to automatically determine the type of a variable, expression, or function return value based on its assigned value, reducing the need for explicit type annotations.

---

## Q2. What is Type Annotation?

**Answer:**  
Type Annotation is the explicit declaration of a type using the `:` syntax, such as `let age: number = 20;`.

---

## Q3. What is the difference between Type Inference and Type Annotation?

| Type Inference | Type Annotation |
|----------------|-----------------|
| Type is determined automatically | Type is specified manually |
| Less code | More explicit |
| Cleaner syntax | Better for APIs and complex code |
| Best for obvious local variables | Best for function parameters, return types, and declarations without initialization |

---

## Q4. Does TypeScript infer function parameter types?

**Answer:**  
No. Function parameters should usually be explicitly annotated. Without annotations, they may become `any` (or produce an error when `noImplicitAny` is enabled).

---

## Q5. Should we always write explicit types?

**Answer:**  
No. Prefer type inference for simple local variables and use explicit annotations where they improve readability, enforce contracts, or are required.

---

## Q6. What is Type Widening?

**Answer:**  
Type Widening is when TypeScript infers a broader type (e.g., `string` instead of `"Hello"`) for mutable values like `let`. For `const`, it often infers the exact literal type.

---

# Summary

- **Type Inference** allows TypeScript to automatically determine types.
- **Type Annotation** lets developers explicitly define types.
- Use inference for simple local variables.
- Use annotations for function parameters, return types, and variables declared without initial values.
- Type inference reduces boilerplate, while annotations improve clarity and maintainability.

---

# Cheat Sheet

## Type Inference

```typescript
let name = "John";      // string
let age = 20;           // number
let active = true;      // boolean
```

---

## Type Annotation

```typescript
let name: string = "John";
let age: number = 20;
let active: boolean = true;
```

---

## Use Type Inference When

- Local variables
- Obvious values
- Arrays with known types
- Simple objects

---

## Use Type Annotation When

- Function parameters
- Function return types (especially exported APIs)
- Variables without initial values
- Class properties
- Complex object structures

---

## Quick Revision

- Type Inference = TypeScript decides the type.
- Type Annotation = Developer decides the type.
- Prefer inference for simple code.
- Prefer annotations for APIs and reusable code.
- Don't annotate unnecessarily when the inferred type is already clear.