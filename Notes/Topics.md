# TypeScript Syllabus (0 → 1 Year Experience)

> Prerequisite:
> - Good JavaScript knowledge (ES6+)
> - Basic OOP concepts
> - Basic understanding of APIs and asynchronous programming

---

# Module 1 — Introduction to TypeScript

## What is TypeScript?

- Why TypeScript?
- JavaScript vs TypeScript
- Advantages
- Drawbacks
- Compile Time vs Runtime
- Strong Typing
- Static Typing
- Structural Typing

### Learn

- TypeScript Compiler (tsc)
- tsconfig.json
- Compilation Process
- Transpiling
- Source Maps

### Practice

- Install TypeScript
- Compile first TS file
- Configure tsconfig

---

# Module 2 — Type System

## Primitive Types

- string
- number
- boolean
- bigint
- symbol
- null
- undefined

## Special Types

- any
- unknown
- never
- void

### Learn Difference

- any vs unknown
- void vs never
- null vs undefined

### Practice

Create variables using every type.

---

# Module 3 — Type Inference

## Learn

- Type Inference
- Type Annotation
- Best Practices

Example

```ts
let name = "John";

let age: number = 20;
```

Practice:

- Infer types
- Explicit annotations

---

# Module 4 — Arrays & Tuples

## Arrays

```ts
string[]
number[]
boolean[]
```

Generic syntax

```ts
Array<string>
```

## Tuples

```ts
[string, number]
```

Readonly Tuples

Practice:

- Student records
- Coordinates
- API responses

---

# Module 5 — Objects

## Object Types

```ts
const user: {
    name: string
    age: number
}
```

Optional Properties

```ts
age?
```

Readonly Properties

Nested Objects

Practice

- User profile
- Product object
- Company object

---

# Module 6 — Functions

## Function Types

Parameters

Return Types

Optional Parameters

Default Parameters

Rest Parameters

Arrow Functions

Anonymous Functions

Callback Functions

Function Overloads

Practice

- Calculator
- Authentication
- Search API

---

# Module 7 — Type Aliases

```ts
type User = {
    name:string
}
```

Union inside aliases

Nested aliases

Reusable aliases

Practice

- Product
- Employee
- Chat Message

---

# Module 8 — Interfaces

## Learn

Interfaces

Optional properties

Readonly

Method definitions

Extending interfaces

Multiple inheritance

Declaration Merging

Difference

Interface vs Type

Practice

- API Response
- User
- Animal
- Vehicle

---

# Module 9 — Union Types

```ts
string | number
```

Complex unions

Object unions

Literal unions

Practice

Status

```ts
"loading"
"success"
"error"
```

---

# Module 10 — Intersection Types

```ts
type A = {}
type B = {}

A & B
```

Practice

Employee + Address

Product + Inventory

---

# Module 11 — Literal Types

```ts
"male"
"female"

1 | 2 | 3
```

Practice

Role

Theme

Status

Button Variants

---

# Module 12 — Enums

Numeric Enums

String Enums

Const Enums

Enum vs Literal Types

Best Practices

Practice

Roles

Status

Payment Methods

---

# Module 13 — Type Assertions

```ts
as
<>
```

Non-null Assertion

Practice

DOM

API

React refs

---

# Module 14 — Generics (Very Important)

## Generic Functions

```ts
function identity<T>()
```

Generic Arrays

Generic Interfaces

Generic Classes

Generic Constraints

Multiple Generics

Default Generics

Practice

API

Pagination

Response

Repository

Stack

Queue

---

# Module 15 — Utility Types

Must Learn

Partial

Required

Readonly

Pick

Omit

Record

Exclude

Extract

NonNullable

ReturnType

Parameters

ConstructorParameters

InstanceType

Awaited

Practice

CRUD APIs

Forms

Redux

React

---

# Module 16 — Advanced Types

keyof

typeof

in

extends

Indexed Access Types

Mapped Types

Conditional Types

Infer

Template Literal Types

Distributive Conditional Types

Practice

Reusable utility types

API typing

Forms

Dynamic Objects

---

# Module 17 — Classes

Class

Constructor

Properties

Methods

Access Modifiers

public

private

protected

readonly

Static

Abstract

Inheritance

Super

Getter

Setter

Implements

Practice

Bank

School

Employee

---

# Module 18 — Modules

Import

Export

Default Export

Named Export

Re-export

Namespaces (basic understanding)

Path Aliases

Practice

Large project structure

---

# Module 19 — Error Handling

try

catch

finally

Custom Errors

Error Types

Practice

API

Authentication

Validation

---

# Module 20 — Async TypeScript

Promise

Promise Generics

async

await

Typing API Response

Fetch

Axios

Practice

REST APIs

Authentication

Pagination

---

# Module 21 — DOM with TypeScript

HTMLElement

HTMLInputElement

Query Selector

Event Types

MouseEvent

KeyboardEvent

FormEvent

Practice

Todo App

Calculator

Weather App

---

# Module 22 — TypeScript Configuration

tsconfig.json

Important options

strict

strictNullChecks

noImplicitAny

target

module

baseUrl

paths

outDir

rootDir

skipLibCheck

esModuleInterop

moduleResolution

resolveJsonModule

---

# Module 23 — TypeScript with Node.js

Express

Environment Variables

Typing Request

Typing Response

Middleware

JWT

Mongoose Types

Prisma Types

Practice

Authentication API

CRUD API

---

# Module 24 — TypeScript with React

Typing Props

Typing State

Typing Hooks

useState

useReducer

useContext

useRef

useMemo

useCallback

Typing Events

React.FC

Children

ForwardRef

Custom Hooks

Forms

API

Practice

Todo

E-Commerce

Authentication

Dashboard

---

# Module 25 — TypeScript with React Native

Navigation Types

Props

FlatList Types

API Types

Context Types

Redux Toolkit

AsyncStorage

Expo

Native Modules

Practice

Chat App

Social Media App

Food Delivery App

---

# Module 26 — TypeScript with Redux Toolkit

Store Types

Dispatch Types

Selectors

AsyncThunk

Middleware

RTK Query

Practice

Authentication

Cart

Products

Users

---

# Module 27 — Design Patterns

Repository Pattern

Factory Pattern

Singleton

Builder

Dependency Injection

Strategy

Observer

Practice

Real Projects

---

# Module 28 — Project Folder Structure

Types Folder

Interfaces

Models

Services

Repositories

Hooks

Utils

Constants

DTO

Shared

---

# Module 29 — Testing

Jest

Vitest

Mocking

Type-safe Tests

Coverage

---

# Module 30 — Best Practices

Avoid any

Prefer unknown

Use strict mode

Reusable Types

Keep Interfaces Small

Avoid Duplicate Types

Prefer Generics

Type Narrowing

Code Readability

Naming Conventions

Folder Structure

---

# Module 31 — Real World Projects

Beginner

- Calculator
- Todo App
- Notes App

Intermediate

- Weather App
- Expense Tracker
- Blog CMS
- Chat App

Advanced

- E-Commerce
- Social Media
- Video Calling
- Netflix Clone
- WhatsApp Clone
- Banking Dashboard
- Admin Panel

---

# Module 32 — Interview Preparation

## Beginner

- What is TypeScript?
- Why TypeScript?
- Advantages?
- Type Inference
- any
- unknown
- never
- void
- Interfaces
- Types
- Union
- Intersection

---

## Intermediate

- Generics
- Utility Types
- keyof
- typeof
- infer
- extends
- Conditional Types
- Mapped Types
- Declaration Merging
- Module Resolution
- Strict Mode

---

## Advanced

- Deep Generic Questions
- Recursive Types
- Type Manipulation
- Performance
- Build Process
- Compiler
- Declaration Files
- Custom Utility Types

---

# Module 33 — Build These Projects

1. Authentication System

2. E-Commerce Backend

3. Chat Application

4. Expense Tracker

5. Food Delivery App

6. Social Media App

7. WhatsApp Clone

8. Portfolio Dashboard

9. Netflix Clone

10. Admin Dashboard

---

# Module 34 — Libraries to Learn

React

React Native

Redux Toolkit

React Query (TanStack Query)

Axios

Express

NestJS

Prisma

Mongoose

Zod

React Hook Form

React Navigation

Socket.IO

---

# Module 35 — Final Checklist

## Core

- Primitive Types
- Functions
- Objects
- Arrays
- Tuples
- Interfaces
- Type Aliases
- Generics
- Utility Types

## Advanced

- keyof
- typeof
- infer
- Conditional Types
- Mapped Types
- Template Literal Types

## React

- Props
- Hooks
- Events
- API Typing
- Context
- Redux

## Backend

- Express
- NestJS
- Prisma
- Mongoose

## Production

- Folder Structure
- DTOs
- Validation
- Error Handling
- Strict Mode
- Testing
- Performance
- Best Practices

---


# Goal After Completion

By the end of this roadmap, you should be able to:

- Build scalable TypeScript applications.
- Write fully type-safe React and React Native apps.
- Develop Node.js/NestJS APIs with TypeScript.
- Understand advanced type manipulation.
- Follow production-grade folder structures.
- Crack TypeScript interviews for 0–1 year experience.
- Contribute to real-world TypeScript codebases confidently.