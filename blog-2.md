# How Generics Let You Write Reusable, Strictly Typed Code in TypeScript

## Introduction

At some point when writing TypeScript, you'll run into a situation where you want to write a function that works with different types of data — but you don't want to sacrifice type safety to do it. The first instinct is to reach for `any`. That works, but then you lose all the type information and TypeScript can't help you anymore.

Generics are the real solution. They let you write flexible, reusable code that stays fully typed no matter what kind of data you pass in. Once you get comfortable with them, you'll use them constantly.

---

## The Problem Generics Solve

Imagine you're writing a simple function that wraps a value in an array:

```typescript
function wrapInArray(value: number): number[] {
  return [value];
}
```

This works fine for numbers. But what if you want it to work for strings too? You'd have to write another function, or use `any`:

```typescript
function wrapInArray(value: any): any[] {
  return [value];
}
```

Now it works for any type, but the return type is `any[]`. If you pass in a string, TypeScript won't know the result is a `string[]`. You've lost the type connection between input and output.

Generics solve this cleanly.

---

## Writing Your First Generic Function

A generic function uses a type parameter — usually written as `<T>` — that acts as a placeholder for whatever type gets passed in:

```typescript
function wrapInArray<T>(value: T): T[] {
  return [value];
}
```

Now when you call `wrapInArray("hello")`, TypeScript infers that `T` is `string` and knows the return type is `string[]`. When you call `wrapInArray(42)`, it knows the return type is `number[]`. The type flows through automatically.

```typescript
const strings = wrapInArray("hello");  // type: string[]
const numbers = wrapInArray(42);       // type: number[]
```

No type information is lost. No manual annotation needed. TypeScript figures it out from the argument.

---

## Generics with Constraints

Sometimes you need to be flexible, but not completely open-ended. You might want a generic function that only works with objects that have certain properties. This is where constraints come in.

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { id: 1, name: "John Doe", age: 21 };
const name = getProperty(user, "name"); // type: string
const id = getProperty(user, "id");     // type: number
```

The `K extends keyof T` constraint means `K` must be one of the actual keys of `T`. If you try to access a key that doesn't exist on the object, TypeScript catches it at compile time — not at runtime when it's too late.

```typescript
getProperty(user, "email"); // Error: Argument of type '"email"' is not assignable
```

This is exactly the kind of safety you want from a type system.

---

## Generic Interfaces and Classes

Generics aren't just for functions. You can use them on interfaces and classes too, which is where they really start to shine.

A generic interface for an API response might look like this:

```typescript
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}
```

Now you can use this same interface for completely different response shapes:

```typescript
const userResponse: ApiResponse<{ name: string; age: number }> = {
  data: { name: "Alice", age: 25 },
  status: 200,
  message: "Success",
};

const listResponse: ApiResponse<string[]> = {
  data: ["item1", "item2"],
  status: 200,
  message: "Success",
};
```

One interface, used for completely different data shapes, fully typed in each case. This is what keeps large codebases manageable.

A generic class works the same way:

```typescript
class DataStore<T> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  getAll(): T[] {
    return this.items;
  }
}

const numberStore = new DataStore<number>();
numberStore.add(1);
numberStore.add(2);

const stringStore = new DataStore<string>();
stringStore.add("hello");
```

`DataStore` works correctly for any type, and TypeScript enforces type consistency within each instance.

---

## Why This Matters in Real Projects

In a real application, you'll frequently write utility functions, data wrappers, and API handlers that need to work with different shapes of data. Without generics, you end up with one of two bad options: write the same logic multiple times for each type, or use `any` and lose type safety entirely.

Generics give you a third option: write it once, keep it typed, reuse it everywhere. When you build a generic filtering function, a generic pagination wrapper, or a generic form state handler, all of them stay fully typed throughout your application.

---

## Conclusion

Generics are one of those features that feel a bit abstract when you first see them, but once they click, you realize they solve a fundamental problem. They let you build reusable building blocks without sacrificing the type safety that makes TypeScript worth using in the first place.

Start with simple cases — generic functions with a single `T` — and build up from there. Before long, writing `<T>` will feel as natural as writing any other part of a function signature.
