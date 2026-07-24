# Module 5 — Objects in TypeScript (Interview Ready Notes)

> **Difficulty:** ⭐⭐☆☆☆ (Beginner → Intermediate)  
> **Interview Importance:** ⭐⭐⭐⭐⭐  
> **Prerequisites:** TypeScript Basics, Type System

---

# What are Objects in TypeScript?

An **object** is a collection of related data stored as **key-value pairs**.

TypeScript allows us to define the **shape (structure)** of an object using object types.

Unlike JavaScript, TypeScript checks whether an object contains the correct properties and value types during compilation.

```ts
const user = {
    name: "John",
    age: 25
}
```

---

# Why Object Types?

Without TypeScript:

```js
const user = {
    name: "John",
    age: "25" // Wrong but JavaScript allows it
}
```

No error occurs.

With TypeScript:

```ts
const user: {
    name: string
    age: number
} = {
    name: "John",
    age: "25"
}
```

Output

```
Error:
Type 'string' is not assignable to type 'number'
```

TypeScript catches errors before runtime.

---

# Object Type Syntax

General Syntax

```ts
const variable: {
    property1: Type
    property2: Type
}
```

Example

```ts
const user: {
    name: string
    age: number
} = {
    name: "John",
    age: 22
}
```

---

# Type Inference with Objects

TypeScript can infer object types automatically.

```ts
const user = {
    name: "John",
    age: 25
}
```

TypeScript infers

```ts
{
    name: string
    age: number
}
```

Hovering over the variable in VS Code shows its inferred type.

---

# Explicit Object Type

Sometimes we define object types manually.

```ts
const student: {
    name: string
    age: number
    isPassed: boolean
} = {
    name: "Rahul",
    age: 20,
    isPassed: true
}
```

---

# Object Property Types

Every property has its own type.

```ts
const product: {
    id: number
    title: string
    price: number
    inStock: boolean
} = {
    id: 1,
    title: "Laptop",
    price: 55000,
    inStock: true
}
```

---

# Optional Properties

Sometimes every object doesn't have all properties.

Use **?** to make a property optional.

Syntax

```ts
property?: Type
```

Example

```ts
const user: {
    name: string
    age?: number
} = {
    name: "John"
}
```

Valid

```ts
const user1 = {
    name: "John"
}

const user2 = {
    name: "John",
    age: 25
}
```

Invalid

```ts
const user = {
    age: 20
}
```

Error

```
Property 'name' is missing.
```

---

# When to Use Optional Properties?

Examples

- User profile
- API response
- Update forms
- Settings object
- Search filters

Example

```ts
const employee: {
    id: number
    name: string
    department?: string
} = {
    id: 101,
    name: "Alex"
}
```

---

# Readonly Properties

Sometimes properties should never change after object creation.

Use **readonly**.

Syntax

```ts
readonly property: Type
```

Example

```ts
const user: {
    readonly id: number
    name: string
} = {
    id: 1,
    name: "John"
}
```

Changing value

```ts
user.id = 5
```

Output

```
Cannot assign to 'id' because it is a read-only property.
```

Changing other properties

```ts
user.name = "David"
```

Valid

---

# Why Readonly?

Useful for

- Database IDs
- UUIDs
- Employee IDs
- Order IDs
- Created Date

Example

```ts
const product: {
    readonly productId: number
    name: string
} = {
    productId: 1001,
    name: "Phone"
}
```

---

# Nested Objects

Objects can contain other objects.

Example

```ts
const user: {
    name: string
    address: {
        city: string
        state: string
        pincode: number
    }
} = {
    name: "John",
    address: {
        city: "Delhi",
        state: "Delhi",
        pincode: 110001
    }
}
```

Access values

```ts
console.log(user.address.city)
console.log(user.address.state)
```

Output

```
Delhi
Delhi
```

---

# Multiple Nested Levels

```ts
const company = {
    name: "Google",
    location: {
        country: "USA",
        office: {
            city: "California",
            floor: 8
        }
    }
}
```

Access

```ts
company.location.office.city
```

---

# Objects with Arrays

Objects often contain arrays.

```ts
const student = {
    name: "Rahul",
    skills: ["React", "Node", "TypeScript"]
}
```

Typed version

```ts
const student: {
    name: string
    skills: string[]
} = {
    name: "Rahul",
    skills: ["React", "Node"]
}
```

---

# Objects with Function Properties

Objects can contain functions.

```ts
const user: {
    name: string
    greet: () => void
} = {
    name: "John",
    greet() {
        console.log("Hello")
    }
}
```

---

# Combining Optional + Readonly

```ts
const employee: {
    readonly id: number
    name: string
    department?: string
} = {
    id: 101,
    name: "Rahul"
}
```

---

# Real World Example — User Profile

```ts
const user: {
    readonly id: number
    name: string
    email: string
    age?: number
    address: {
        city: string
        state: string
    }
} = {
    id: 1,
    name: "John",
    email: "john@example.com",
    address: {
        city: "Delhi",
        state: "Delhi"
    }
}
```

---

# Real World Example — Product Object

```ts
const product: {
    readonly id: number
    title: string
    price: number
    discount?: number
    stock: number
} = {
    id: 101,
    title: "iPhone",
    price: 85000,
    stock: 12
}
```

---

# Real World Example — Company Object

```ts
const company: {
    name: string
    employees: number
    address: {
        city: string
        country: string
    }
    founder?: string
} = {
    name: "OpenAI",
    employees: 5000,
    address: {
        city: "San Francisco",
        country: "USA"
    }
}
```

---

# Object Type vs any

Bad Practice

```ts
const user: any = {
    name: "John",
    age: "25"
}
```

Good Practice

```ts
const user: {
    name: string
    age: number
} = {
    name: "John",
    age: 25
}
```

---

# Common Mistakes

## Missing Required Property

```ts
const user: {
    name: string
    age: number
} = {
    name: "John"
}
```

Error

```
Property 'age' is missing.
```

---

## Wrong Property Type

```ts
const user = {
    name: "John",
    age: "25"
}
```

Expected

```ts
age: number
```

---

## Extra Properties

```ts
const user: {
    name: string
} = {
    name: "John",
    age: 25
}
```

Error

```
Object literal may only specify known properties.
```

---

## Modifying Readonly Property

```ts
user.id = 10
```

Error

```
Cannot assign to 'id'
```

---

# Best Practices

✅ Give explicit types for complex objects.

✅ Use optional properties when values may not always exist.

✅ Use readonly for immutable data.

✅ Keep object structures consistent.

✅ Prefer interfaces or type aliases for reusable object shapes.

✅ Avoid using `any`.

---

# Interview Questions

### Q1. What is an object type in TypeScript?

An object type defines the structure of an object by specifying property names and their types.

---

### Q2. Why use object types?

- Type safety
- Better IntelliSense
- Compile-time error checking
- Easier maintenance

---

### Q3. Difference between optional and readonly properties?

| Optional (?) | Readonly |
|--------------|----------|
| Property may or may not exist | Property exists but cannot be modified |
| Used for optional data | Used for immutable data |

---

### Q4. What does `?` mean?

It marks a property as optional.

```ts
age?: number
```

---

### Q5. What does `readonly` do?

It prevents reassignment after initialization.

---

### Q6. Can objects contain other objects?

Yes.

Example

```ts
const user = {
    address: {
        city: "Delhi"
    }
}
```

---

### Q7. Can objects contain arrays?

Yes.

```ts
const student = {
    skills: ["React", "Node"]
}
```

---

### Q8. Can objects contain functions?

Yes.

```ts
const person = {
    greet() {
        console.log("Hello")
    }
}
```

---

# Summary

- Objects store related data using key-value pairs.
- TypeScript object types define the exact structure of an object.
- Optional properties (`?`) allow properties to be omitted.
- Readonly properties prevent reassignment.
- Nested objects help model real-world data.
- Objects can include arrays, functions, and other objects.
- Explicit object typing improves readability and type safety.
- Use interfaces or type aliases for reusable object structures.