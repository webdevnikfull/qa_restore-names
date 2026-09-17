# 🗂️ QA: Restore Names - Data Recovery Validation Suite

> ### A unit testing suite built with **Jest** to validate a data recovery script designed to repair corrupted database records.

This repository is a professional showcase of **Software Quality Assurance (QA)** techniques applied to data mutation and state side-effects. It focuses on architecting automated tests for the `restoreNames` function, which recovers lost data fields after a simulated database failure.

---

## 🎯 System Under Test (SUT)

Due to a database failure, some user records have lost their `firstName` values. Fortunately, the integrity of the `fullName` field remained intact. 

The `restoreNames` function is a data-patching script that accepts an array of `users` objects. Its purpose is to parse the `fullName` and dynamically restore the `firstName` for any user where the field is either missing or strictly equal to `undefined`[cite: 6].

**Critical Architectural Detail:** The function operates via **Object Mutation**. It does not return a new array; it modifies the input array directly and returns nothing (a `void` function)[cite: 6].

**Example of Expected State Mutation:**
```javascript
// Input State
const users = [
  { firstName: undefined, lastName: 'Holy', fullName: 'Jack Holy' }, // undefined field[cite: 6]
  { lastName: 'Adams', fullName: 'Mike Adams' },                     // missing field entirely[cite: 6]
];

restoreNames(users); // Function executes (returns nothing)[cite: 6]

// Assert Output State
// users[0].firstName === 'Jack'[cite: 6]
// users[1].firstName === 'Mike'[cite: 6]
