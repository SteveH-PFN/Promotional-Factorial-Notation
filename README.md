# Promotional Factorial Notation (PFN)

**A large number notation system based on factorials and recursive operations**  
Developed by **Steve H.** (2025)  
Licensed under the MIT License

---

## 📘 Overview

Promotional Factorial Notation (PFN) is a large-number notation system that builds on the explosion of iterated factorial operations. Rather than following the traditional hyperoperation path (like Knuth's up-arrows), PFN creates enormous values through controlled, symbolic factorial layering with promotion levels that represent recursive depth.

The notation balances human readability with extraordinary growth potential, even faster growing when paired with extensions like **Fractal Mode**.

---

## 🔧 Core Mechanics

### 🧱 Base Operations (B)

A PFN expression starts with a whole number followed by one or more factorials:

```
3!   = 6  
3!!  = (3!)! = 6! = 720
```

- Chained factorials are evaluated **left to right**, one at a time.
- The starting value is called **B**, and is referenced in all subsequent operations.
- Note: B is dynamic — it always represents the evaluated result of the whole number plus all factorials processed up to that point. As PFN symbols are expanded, B grows rapidly and influences subsequent expansion depth.

---

### 🪜 Promotion Levels `($n)`

($1) is factored by applying the factorial function to the entire solvable expression (B) up to that point.
- ℹ️ This is equivalent to appending one factorial sign (!). 

Each `($n)` above 1 represents a **promotion level** that indicates how many lower of the next lower will be inserted into the expression:

| Symbol  | Description                          |
|---------|--------------------------------------|
| `($1)`  | Equivalent to adding one factorial   |
| `($2)`  | Expands to B copies of `($1)`        |
| `($3)`  | Expands to B copies of `($2)`        |
| ...     | And so on                            |


> Think of promotions as **symbolic placeholders** for recursive depth that explode into lower levels when evaluated.

---

### Proper PFN Expression:

- A proper PFN expression consists of a base value **B**, optionally followed by one or more **promotion levels in ascending order**, then any optional $dyn references (explained later).

- PFN is effectively re-written in ascending order at each step of the sequence due to the promotion levels expanding in-place. This can also be thought of as lazy substitution, macro expansion, recursive reduction, etc. 

Valid: 
```
3!($2)($2)($2)
3!($2)($3)($4)
3!($20)($dyn)
3!($200)($dyn)($dyn)
```
Not valid:
```
3!($3)($4)($2)
3!($dyn)($30000)
($4)3!
```

### 🧪 Example: Basic Demotion

```
3!($1) = 3!! = 720

3!($2)  
= 3! → 6  
= 6 instances of `($1)` expanded in the expression
= 3!($1)($1)($1)($1)($1)($1)
= 3!!!!!!!
```

- Note: ($1) is the only promotion you can bulk mutate directly, as they will always represent a single factorial, added to the end of your current base (B). 
- Note: In examples, base values like 3! = 6 are shown to illustrate structure, not to suggest full evaluation — factorial chains quickly become computationally unmanageable and are treated symbolically beyond basic steps.

---

### 🔄 Dynamic Evaluation Symbol `($dyn)`

`$dyn` is a special symbol that **resolves to the current expression value at the time it is reached and must come after all static promotions**.

```
3!!($dyn) → 3!! = 720, so $dyn becomes ($720)
3!($3)($dyn) → We must solve everything to left of dyn to know it's value. 
```

---

### ⏩ Repeater Symbol `>>`

The `>>` symbol allows repeated appending of unresolved `$dyn` symbols or complex blocks:

- `>> n` means: repeat `$dyn` **n** times  
  ```
  3!($dyn) >> 5  
  → 3!($dyn)($dyn)($dyn)($dyn)($dyn)
  ```

- `>> dyn` means: compute the current expression value and append that **many** `$dyn` symbols
- Can be used on more advanced blocks, such as:
  ```
  3!((($dyn)>>dyn) >> dyn)
  ```
  -Which would result in: 
   ```
  3!(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)
  ```
  This means "Evaluate the second 'dyn' in the first parenthesis set, and apply this many unsolved ($dyn) promotions to the sequence.
  After resolving all of those, proceed to the second block, and re-evaluate the expression for the new 'dyn'."
---

## 📐 First Simplified Form

When working with high promotion levels, and large bases *First Simplified Form* helps us understand the structure without evaluating the base:

### General Formula:

```
B!($L) → B!(($1)^B)(($2, $3...$L-1)^(B-1))
```

### Alternate Notations:

- `B! · B×($1) · (B−1)×($2→$L−1)`
- `B! · ($1)×B · ($2-$L−1)×(B−1)`
- `B! · [B:$1] · [B−1:$2-$L−1]`
- Programmatic:  
  `B! + repeat($1, B) + repeat(range($2, $L−1), B−1)`

### Example:
For `3!($20)`:

- `B = 3! = 6`
- `L = 20`

Simplified form:
```
3! ($1)^6 ($2, $3...$19)^5
```

Expanded(ish):
```
3!($1)($1)($1)($1)($1)($1)($2)($2)...($19)($19)($19)($19)($19)
```

---
# PFN: First Simplified Form – Proof Example

### 📎 Why This Works: Step-by-Step Proof (3!($6))

To understand the formula structure, let's walk through the demotion process of `3!($6)` manually.

**Step 1: Evaluate the base.**  
`3! = 6`, so:
```
3!($6)
→ 3!($5)($5)($5)($5)($5)($5)
The single 6 is "demoted" to B number of ($5)
```

**Step 2: Evaluate the first `($5)`**
- Current total (B) = 6
- The first `($5)` becomes **6 `($4)`s**
```
3!($4)($4)($4)($4)($4)($4)($5)($5)($5)($5)($5)
```

**Step 3: Evaluate the same down the line, starting with the first `($4)`**
- 3!($4)($4)($4)($4)($4)($4)($5)($5)($5)($5)($5)
- → 3!($3)($3)($3)($3)($3)($3)($4)($4)($4)($4)($4)($5)($5)($5)($5)($5)
- → 3!($2)($2)($2)($2)($2)($2)($3)($3)($3)($3)($3)($4)($4)($4)($4)($4)($5)($5)($5)($5)($5)
- → 3!($1)($1)($1)($1)($1)($1)($2)($2)($2)($2)($2)($3)($3)($3)($3)($3)($4)($4)($4)($4)($4)($5)($5)($5)($5)($5)

**Fin:**

The key pattern here is:
- The **first `($6)`** produces **B = 6** copies of `($5)` - the ($6) will never be seen again. 
- One `($5)` then expands into B number of ($4), one ($4) into B number of 3, and so on. 

Hence:
```
B($L) → B(($1)^B) ($2, $3...$L−1)^(B−1)
```

The `($1)` promotion appears **B times** (because it's at the bottom and factored into last), and each subsequent level appears **B−1 times** due to nested expansions and the demoting of the lowest level promotion available in the stack (Remember, PFN is always in ascending promotion order, even after a demotion). This recursive pattern naturally emerges from how symbols expand and how the total influences expansion depth.

## ⚙️ Processing Rules

- **Sequential Processing**: PFN processes one symbol at a time, left to right
- **Ascending Order**: Higher-level promotions must appear after lower-level ones
- **One-at-a-Time Expansion**: `($n)` expands into the **current total base** number of `($n−1)`s **at the time it's reached**

---

## 🌳 Extension: Fractal Mode (Fractorials, if you're feeling cheeky.)

Fractal Mode is a recursive multiplication model that works as an extension to PFN.

### Rules:

1. Create a standard factorial sequence, such as 4x3x2x1
2. For every value >1, apply a factorial to that number
```
4x3(x2[x1]x1)x2x1
```
4. The result is the **product** of all values across all branches
5. The fractal is considered complete when all branches of all factorials terminate at 1. 

---

### Growth Formula of fractal factorials 

Let `F(n)` be the Fractal Mode value at `n`:

```
F(1) = 1
F(n) = (F(n-1)^2 × n) / (n - 1)  , for n >= 1
```
Example going from fractal 4 to fractal 5:
```
Fractal 4 = 4x3(x2[x1]x1)x2x1 = 48
For n = 5, F(n-1) = 48
Fractal 5 = (((48) ^ 2) * 5)/(5-1) = 2880
```
This is due to n+1 having the same basic structure, then you multiply by the new n, and divide to remove a duplicate reference to the n-1 node, which now has two branches, but only one base. 
### Growth Properties:

- From `n = 5` onward, `log₁₀(F(n))` roughly **doubles per step** (Needs more thorough testing)
- `Fractal(50)` → ~10²⁹ digits  
- `Fractal(2880)` → ~10^(10^881)

---


## 🔼 Comparison with Other Notations

PFN mirrors **hyperoperation structure**, replacing exponentiation with **factorial recursion**:

| PFN        | Structure                      | Knuth Arrows |
|------------|--------------------------------|---------------|
| `($1)`     | One factorial                  | `↑`           |
| `($2)`     | B repeated factorials          | `↑↑`          |
| `($3)`     | Repeat ($2) B times            | `↑↑↑`         |
| `($4)`     | Repeat ($3) B times            | `↑↑↑↑`        |

> PFN doesn't match the **values** of hyperoperations, but mirrors their **recursive structure** — replacing `^` with `!`.

---

## 💻 Implementation

**Coming soon:**  
- Pseudocode  
- Python/JS implementations

---

## 👤 Contributors

- **Steve H.** — Creator and primary designer  

---

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

---

> This documentation is a work in progress.  
> Contributions, clarifications, and expansions are welcome.
