
### What is TypeScript?
TypeScript is a programming language developed and maintained by Microsoft.
It is a strict `syntactical superset` of JavaScript and adds optional static typing to the language.

### Q. **Where/How does typescript code run?**
Typescript code never runs in your browser. Your browser can only understand `javascript`.

1. Javascript is the runtime language (the thing that actually runs in your browser/nodejs runtime)
2. Typescript is something that compiles down to javascript
3. When typescript is compiled down to javascript, you get `type checking` (similar to C++). If there is an error, the conversion to Javascript fails.

---

## How to use typescript in code?
 **Step 1 - Install tsc/typescript globally**
```bash
npm install -g typescript
```

**Step 2 - Initialize an empty Node.js project with typescript**
```bash
npm init -y
npx tsc --init
```

**Step 3 - Create a test.ts file**
```jsx
const x: String = "Hello World";
console.log(x);
```

**Step 4 - Compile the ts file to js file**
```bash

tsc -b
```

**Step 5 - Explore the newly generated js file**

---

## TS types
Run this code and check all
![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code.png)

## Function

![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%201.png)


---

### Object
### **Interface for object types**

![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%202.png)

---

### type as object type
![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%203.png)

---

## interface vs type

| interface | type |
| --- | --- |
| It is a form of syntax. | It is a collection of data types. |
| It uses the “interface” keyword for declaring an interface. | Types are more flexible. |
| it cannot be used with other types of declaration. | It is also used for types such as primitives, unions, and tuples. |

## Enums
Enums(short for enumerations) in TypeScript are a feature that allows you to define a set of named constants.
The concepts behind an enumeration is to create a human-readable way to represent a set of constant values, which might otherwise be represented as numbers or strings

 Direction Game
![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%204.png)

---

### Real example
![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%205.png)

---
## **Generics**

![code1.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code1.png)


## Pick
**`Pick`** allows you to create a new type by selecting a set of properties (**`Keys`**) from an existing type (**`Type`**).
Imagine you have a User model with several properties, but for a user profile display, you only need a subset of these properties.

![code.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code%206.png)

## Partial
**`Partial`** makes all properties of a type optional, creating a type with the same properties, but each marked as optional.
### Brute Force way
![code1.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code1%201.png)

### Better Approach
![code2.png](TypeScript%20cf9ff40b04cf4bf48cb85f1d6f5a69c3/code2.png)
