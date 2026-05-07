# B7A1 — Advanced Problem Solving with TypeScript & OOP

This repository contains my submission for the **B7A1 Assignment** from the Programming Hero Full Stack Web Development course. It covers fundamental to intermediate TypeScript concepts including type guards, generics, interfaces, class inheritance, and utility types.

---

## 📁 File Structure

```
├── solutions.ts     # All 7 coding problems in a single file
├── blog-1.md        # Blog: any vs unknown and type narrowing
├── blog-2.md        # Blog: Generics in TypeScript
└── README.md        # Project overview
```

---

## 🧩 Problems Covered

| # | Problem | Concept |
|---|---------|---------|
| 1 | `filterEvenNumbers` | Array filtering |
| 2 | `reverseString` | String manipulation |
| 3 | `checkType` | Union types & type guards |
| 4 | `getProperty` | Generics with keyof constraints |
| 5 | `toggleReadStatus` | Interfaces & object spreading |
| 6 | `Person` & `Student` classes | OOP inheritance |
| 7 | `getIntersection` | Set-based array intersection |

---

## 📝 Blog Posts

**Blog 1:** `any` vs `unknown` — why `any` is a type safety hole, how `unknown` forces responsible type handling, and what type narrowing looks like in practice.

**Blog 2:** Generics — how generic functions, interfaces, and classes let you write reusable code that stays fully typed regardless of the data structure passed in.

---

## 🛠 Technologies Used

- TypeScript
- Node.js (for running TypeScript via `ts-node`)

---

## 🚀 How to Run

**1. Install dependencies**

```bash
npm install -g ts-node typescript
```

**2. Run the solution file**

```bash
ts-node solutions.ts
```

**3. Compile to JavaScript (optional)**

```bash
tsc solutions.ts
node solutions.js
```

---

## 👤 Author

Submitted as part of the Programming Hero Full Stack Web Development — Batch 7 coursework.
