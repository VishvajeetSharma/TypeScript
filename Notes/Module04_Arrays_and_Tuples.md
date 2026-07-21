# Module 4 — Arrays & Tuples

> **Difficulty:** Beginner  
> **Interview Importance:** ⭐⭐⭐⭐⭐  
> **Prerequisite:** Module 3 — Type Inference & Type Annotation

---

# What are Arrays?

An **Array** is a collection of multiple values stored in a single variable.

In TypeScript, arrays are **typed**, meaning all elements in the array must follow the specified type.

Unlike JavaScript, TypeScript checks that only valid values are added to the array at **compile time**.

Example:

```typescript
let numbers: number[] = [10, 20, 30];
```

Only numbers are allowed.

---

# Why Do We Need Typed Arrays?

Consider JavaScript:

```javascript
let numbers = [10, 20, 30];

numbers.push("Hello");
```

This is allowed in JavaScript.

Now imagine later:

```javascript
numbers.reduce((a, b) => a + b);
```

Unexpected results or runtime bugs may occur.

With TypeScript:

```typescript
let numbers: number[] = [10, 20, 30];

numbers.push("Hello");
```

Compilation Error:

```
Argument of type 'string'
is not assignable to parameter of type 'number'.
```

TypeScript prevents invalid values from being added.

---

# Array Syntax

There are **two ways** to define arrays in TypeScript.

## Method 1 — Square Bracket Syntax (Recommended)

```typescript
let numbers: number[] = [10, 20, 30];
```

General Syntax:

```typescript
let arrayName: Type[] = [];
```

Example:

```typescript
let fruits: string[] = ["Apple", "Banana", "Mango"];

let marks: number[] = [90, 80, 70];

let isOnline: boolean[] = [true, false, true];
```

---

## Method 2 — Generic Syntax

TypeScript also supports generic array syntax.

General Syntax:

```typescript
let arrayName: Array<Type> = [];
```

Example:

```typescript
let fruits: Array<string> = ["Apple", "Banana"];

let marks: Array<number> = [90, 80, 70];

let flags: Array<boolean> = [true, false];
```

Both syntaxes are exactly equivalent.

```typescript
string[]
```

is the same as

```typescript
Array<string>
```

---

# string[]

Stores only strings.

```typescript
let cities: string[] = [
    "Delhi",
    "Mumbai",
    "Lucknow"
];
```

Allowed:

```typescript
cities.push("Pune");
```

Not allowed:

```typescript
cities.push(100);
```

Compilation Error.

---

# number[]

Stores only numbers.

```typescript
let prices: number[] = [200, 300, 500];
```

Operations:

```typescript
prices.push(600);

prices.pop();

prices.includes(300);
```

---

# boolean[]

Stores only boolean values.

```typescript
let permissions: boolean[] = [
    true,
    false,
    true
];
```

---

# Empty Arrays

Explicit annotation is recommended.

```typescript
let users: string[] = [];
```

Without annotation:

```typescript
let users = [];
```

The inferred type depends on compiler settings and context, which may not be what you expect.

---

# Array Type Inference

TypeScript can infer array types.

Example:

```typescript
let colors = [
    "Red",
    "Green",
    "Blue"
];
```

Type inferred:

```typescript
string[]
```

---

Another example:

```typescript
let scores = [10, 20, 30];
```

Type:

```typescript
number[]
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

This is called a **Union Type**.

---

# Common Array Methods

## push()

Adds an element.

```typescript
let fruits: string[] = ["Apple"];

fruits.push("Orange");
```

---

## pop()

Removes the last element.

```typescript
fruits.pop();
```

---

## shift()

Removes the first element.

```typescript
fruits.shift();
```

---

## unshift()

Adds an element at the beginning.

```typescript
fruits.unshift("Mango");
```

---

## includes()

Checks whether a value exists.

```typescript
fruits.includes("Apple");
```

Returns:

```typescript
boolean
```

---

## map()

Transforms every element.

```typescript
let prices = [100, 200];

let discounted = prices.map(price => price * 0.9);
```

---

## filter()

Returns matching elements.

```typescript
let scores = [80, 45, 90];

let passed = scores.filter(score => score >= 50);
```

---

## find()

Returns the first matching element.

```typescript
let users = ["Rahul", "Aman"];

users.find(user => user === "Rahul");
```

---

# Multidimensional Arrays

Arrays can contain other arrays.

```typescript
let matrix: number[][] = [
    [1, 2],
    [3, 4]
];
```

Meaning:

```
number[][]
```

An array of number arrays.

---

# What are Tuples?

A **Tuple** is a special type of array where:

- The number of elements is fixed.
- The order of elements matters.
- Each position can have a different type.

Example:

```typescript
let student: [string, number] = [
    "Rahul",
    21
];
```

Meaning:

- First value → string
- Second value → number

---

# Why Use Tuples?

Arrays:

```typescript
(string | number)[]
```

can contain values in any order.

```typescript
["Rahul", 21]

[21, "Rahul"]

["Rahul", 21, 90]
```

All are possible depending on the array type.

Tuples enforce both **order** and **length**.

---

# Tuple Syntax

General Syntax:

```typescript
let variable: [
    Type1,
    Type2,
    Type3
];
```

Example:

```typescript
let employee: [number, string] = [
    101,
    "Rahul"
];
```

---

# Tuple Example

```typescript
let product: [string, number, boolean] = [
    "Laptop",
    60000,
    true
];
```

Meaning:

```
Product Name
Price
In Stock
```

---

# Accessing Tuple Values

```typescript
let user: [string, number] = [
    "Rahul",
    25
];

console.log(user[0]);

console.log(user[1]);
```

Output:

```
Rahul

25
```

---

# Updating Tuple Values

```typescript
let student: [string, number] = [
    "Aman",
    20
];

student[1] = 21;
```

Allowed because the type matches.

Incorrect:

```typescript
student[1] = "Twenty One";
```

Compilation Error.

---

# Readonly Tuples

Sometimes tuple values should never change.

Use `readonly`.

Syntax:

```typescript
readonly [
    Type1,
    Type2
]
```

Example:

```typescript
let coordinate: readonly [number, number] = [
    10,
    20
];
```

Incorrect:

```typescript
coordinate[0] = 50;
```

Compilation Error.

---

# Array vs Tuple

| Array | Tuple |
|--------|-------|
| Same type of elements | Different types allowed |
| Variable length | Fixed length |
| Order usually doesn't matter | Order matters |
| Flexible | Strict structure |
| Example: `string[]` | Example: `[string, number]` |

---

# Tuple vs Object

Tuple:

```typescript
let user: [string, number] = [
    "Rahul",
    22
];
```

Object:

```typescript
let user = {
    name: "Rahul",
    age: 22
};
```

Use:

- **Tuple** for short, positional data.
- **Object** when property names improve readability.

---

# Real-World Examples

## Student Record (Tuple)

```typescript
let student: [number, string, number] = [
    101,
    "Rahul",
    95
];
```

Meaning:

```
Student ID

Name

Marks
```

---

## Coordinates

```typescript
let location: [number, number] = [
    28.6139,
    77.2090
];
```

Meaning:

```
Latitude

Longitude
```

---

## RGB Color

```typescript
let rgb: [number, number, number] = [
    255,
    128,
    64
];
```

---

## Product List

```typescript
let products: string[] = [
    "Laptop",
    "Phone",
    "Watch"
];
```

---

## Shopping Cart Prices

```typescript
let prices: number[] = [
    1000,
    500,
    800
];
```

---

## API Response (Tuple)

Some APIs return positional arrays.

```typescript
let apiResponse: [number, string] = [
    200,
    "Success"
];
```

Meaning:

- Status Code
- Message

---

# Practice

## Practice 1 — Student Records

Create a tuple representing a student.

```typescript
let student: [number, string, number] = [
    101,
    "Rahul",
    92
];
```

---

## Practice 2 — Coordinates

Represent latitude and longitude.

```typescript
let coordinates: [number, number] = [
    28.6139,
    77.2090
];
```

---

## Practice 3 — API Response

Represent an API response using a tuple.

```typescript
let response: [number, string] = [
    200,
    "Success"
];
```

---

## Practice 4 — Arrays

Create arrays for:

```typescript
let names: string[] = [
    "Rahul",
    "Aman",
    "Priya"
];

let marks: number[] = [
    80,
    90,
    95
];

let attendance: boolean[] = [
    true,
    false,
    true
];
```

---

## Practice 5 — Generic Syntax

Rewrite using generic arrays.

```typescript
let names: Array<string> = [
    "Rahul",
    "Aman"
];

let marks: Array<number> = [
    80,
    90
];
```

---

# Best Practices

- Prefer `Type[]` syntax for simple arrays because it is shorter and more readable.
- Use `Array<Type>` when working with complex generic types.
- Use tuples only when the number and order of elements are fixed.
- Use `readonly` tuples for immutable data.
- Prefer objects instead of long tuples with many elements.
- Explicitly type empty arrays.

---

# Common Mistakes

## Mistake 1

Mixing types in a typed array.

```typescript
let numbers: number[] = [10, 20];

numbers.push("Hello");
```

---

## Mistake 2

Using tuples when objects are more readable.

```typescript
["Rahul", 22, "Delhi", true]
```

Better:

```typescript
{
    name: "Rahul",
    age: 22,
    city: "Delhi",
    isActive: true
}
```

---

## Mistake 3

Changing readonly tuples.

```typescript
readonly [number, number]
```

Values cannot be modified.

---

## Mistake 4

Confusing arrays with tuples.

Arrays:

```typescript
string[]
```

Tuples:

```typescript
[string, number]
```

---

# Common Interview Questions

## Q1. What is the difference between an array and a tuple?

**Answer:**  
An array stores elements of the same type and usually has a variable length, while a tuple has a fixed length, preserves element order, and can contain different types at different positions.

---

## Q2. What is the difference between `string[]` and `Array<string>`?

**Answer:**  
There is no functional difference. Both represent an array of strings. `string[]` is shorter and commonly preferred, while `Array<string>` is useful in generic type expressions.

---

## Q3. What is a readonly tuple?

**Answer:**  
A readonly tuple cannot be modified after creation. Attempting to change its values results in a compile-time error.

Example:

```typescript
let point: readonly [number, number] = [10, 20];
```

---

## Q4. Can tuples store different types?

**Answer:**  
Yes. Each position in a tuple can have its own type.

Example:

```typescript
let employee: [number, string];
```

---

## Q5. When should you use a tuple instead of an object?

**Answer:**  
Use a tuple for small, fixed, positional data such as coordinates or `[statusCode, message]`. Use an object when property names improve readability or when the data structure is more complex.

---

## Q6. Can TypeScript infer array types?

**Answer:**  
Yes. If all elements have the same type, TypeScript automatically infers the array type.

Example:

```typescript
let names = ["A", "B"];
```

Type inferred:

```typescript
string[]
```

---

# Summary

- Arrays store collections of values of the **same type**.
- Arrays can be written using `Type[]` or `Array<Type>`.
- Tuples are fixed-length arrays with **ordered elements** that may have different types.
- Readonly tuples prevent modification after creation.
- Arrays are ideal for lists, while tuples are ideal for small, structured positional data.

---

# Cheat Sheet

## Arrays

```typescript
let names: string[] = [];

let marks: number[] = [];

let flags: boolean[] = [];
```

---

## Generic Arrays

```typescript
let names: Array<string> = [];

let marks: Array<number> = [];
```

---

## Tuple

```typescript
let student: [string, number] = [
    "Rahul",
    20
];
```

---

## Readonly Tuple

```typescript
let point: readonly [number, number] = [
    10,
    20
];
```

---

## Quick Revision

- `string[]` = Array of strings.
- `number[]` = Array of numbers.
- `boolean[]` = Array of booleans.
- `Array<T>` = Generic array syntax.
- Tuple = Fixed length + ordered + different types allowed.
- `readonly` tuple = Immutable tuple.
- Arrays → Lists of similar items.
- Tuples → Small structured positional data.