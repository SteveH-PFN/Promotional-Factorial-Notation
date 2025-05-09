
# Promotional Factorial Notation (PFN)

**A large number notation system based on factorials and recursive operations**  
Developed by **Steve H.** (2025)  
Licensed under the MIT License

---

## 📘 Overview

Promotional Factorial Notation (PFN) is a large number notation system that reimagines factorial chaining in a symbolic language of recursive growth. Instead of using hyperoperations like Knuth's up-arrows, PFN creates massive values through controlled symbolic expansion, layering factorials and recursive structures called *promotion levels*.

PFN balances readability and expressiveness, especially when extended with **Fractal Mode**, a recursive expansion mechanic that pushes PFN to a next level, and has some cool findings.

---

## 🧮 Symbol Reference Table

| Symbol         | Description                                                          |
|----------------|----------------------------------------------------------------------|
| `!`            | Standard factorial                                                   |
| `!!`, `!!!`    | Chained factorials (evaluated left to right)                         |
| `($n)`         | Promotion level: expands into `B` copies of `($n−1)`                 |
| `($dyn)`       | Resolves to current B value at time of evaluation                    |
| `^`            | Repeat previous symbol a specified number of times                   |
| `>>`           | Repeat previous block a specified number of times (used with dyn)                  |


---

## 🔧 Core Mechanics

### 🧱 Base Operations (B)

A PFN expression begins with a whole number followed by chained factorials:

```
3!   = 6
3!!  = (3!)! = 6! = 720
```

- Factorials are evaluated **left to right**.
- The **base** `B` is always the running result of the initial value plus any chained factorials.
- As promotion symbols expand, they reference the current value of `B`, which grows rapidly and fuels deeper recursion.

---

### 🪜 Promotion Levels `($n)`

Promotion symbols are what make PFN explode.

- `($1)` = Append one factorial (!)
- `($2)` = Expand into `B` copies of `($1)`
- `($3)` = Expand into `B` copies of `($2)`
- And so on...

| Promotion | Meaning                                     |
|-----------|---------------------------------------------|
| `($1)`    | One factorial (!), applied to current value |
| `($2)`    | `B` copies of `($1)`                        |
| `($3)`    | `B` copies of `($2)`                        |

> Think of each `($n)` as a symbolic **macro** that expands into lower levels using the current `B`.

#### Example:

```
3!($2)
→ 3! = 6
→ Insert 6 copies of ($1)
→ 3!($1)($1)($1)($1)($1)($1)
→ 3!!!!!!!
```

---

## 🔄 Dynamic Symbol `$dyn`

`$dyn` resolves to the current value of the full expression when it's reached.

- Must appear **after all static promotions**

```
3!!($dyn)
→ 3!! = 720, so `$dyn` becomes `($720)`
```

You can also use `>>` to repeat it:

```
3!($dyn) >> 5
→ 3!($dyn)($dyn)($dyn)($dyn)($dyn)
```

Nested usage allows wild recursion of entire blocks of logic using dyn:

```
3!(($dyn)>>dyn) >> dyn
→ 3!(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)(($dyn)>>dyn)
```
Steps for above:
- Evaluate base: 3! = 6 => B = 6
- Start with the outermost '>>dyn'
- Since dyn = 6, repeat the block to the left of it—"(($dyn)>>dyn)"—six times
- Each copy of that block will be evaluated independently, at the time it is reached
- Solving each block involves resolving dyn again, inserting that many unsolved ($dyn)s

---

## ✅ Valid PFN Syntax

Proper PFN expressions:
- Start with a whole number and optional factorials
- Follow with promotions in **ascending** order
- Use `$dyn` **after** all static promotions

```
✅ Valid:
3!($2)($2)($2)
3!($2)($3)($4)
3!($20)($dyn)

❌ Invalid:
3!($3)($4)($2)      ← Not ascending
($4)3!              ← Promotions must follow a base
3!($dyn)($30000)    ← Static symbol cannot follow dyn
```

---

## 🔬 First Simplified Form

PFN expressions expand recursively, but a pattern emerges that helps us describe the structure without full evaluation.

**General Formula:**
```
B!($L) → B! · ($1)^B · ($2 → $L−1)^(B−1)
```

**Alternate Notations:**
```
- B! · B×($1) · (B−1)×($2→$L−1)
- B! + repeat($1, B) + repeat(range($2, $L−1), B−1)
```

### 🔍 Worked Example: `3!($4)`

- `3! = 6` ⇒ `B = 6`, `L = 4`

So:
```
3!($4) → 3!($1)^6 ($2)^5 ($3)^5
```

That means:
- 6 copies of `($1)`
- 5 copies each of `($2)` and `($3)`
- Total demotion happens **one layer at a time**, using the current B at each step

---

## 🌳 Fractal Mode (Fractorials, if you're feeling cheeky)

Fractal Mode is an optional PFN extension that reinterprets each number as a **self-branching factorial tree**.

### Rules:

1. Start with any `n`
2. Create descending factorial chain: `n, n-1, ..., 1`
3. For every value >1, recursively treat it like its own factorial tree
4. Multiply **all values** across all branches

### Example:
```
Fractal(4): 4×3×(2[×1]×1)×2×1 = 48
Fractal(5): (((48)^2)×5)/4 = 2880
```


### 📈 Growth Formula

```
F(1) = 1  
F(n) = (F(n−1)^2 × n) / (n − 1), for n ≥ 1
```

> 🧠 **Intuition Behind the Formula:**

- When building `Fractal(n+1)`, the structure of `Fractal(n)` appears **twice**:
  - Once directly
  - Once as a sub-branch beneath the new root `n+1`
  
- This results in the `n` node being **double-counted**.

- To correct for this:
  - ✅ **Divide by `(n−1)`** to remove the duplicate reference
  - ✅ **Multiply by `n`** to add the new top-level node

> 📌 Fractal growth is **not just exponential**, but **structurally recursive**—
> each layer symmetrically replicates and nests the prior.

---

### 🔢 Approximate Growth

- `Fractal(50)` ≈ **~10^29 digits**
- `Fractal(2880)` ≈ **~10^(10^881)**
- From `n = 5` onward,  
  `log₁₀(F(n))` **asymptotically doubles** with each step
> ℹ️ **What does 'asymptotically doubles' mean?**  
> As n increases, the number of digits in F(n) grows so rapidly that it causes log₁₀(F(n)) to be just over double every time, closer to exactly 2 as you go up.
> At n = 30, log₁₀(F(n)) is still growing faster than exactly 2x—but by less than a billionth.
> The farther you go, the more exact that doubling becomes.

> 🧨 Fractorials are brutally effective growth tools when used inside PFN expressions.


---

## 🔁 Comparison with Hyperoperations

PFN mirrors the recursive **structure** of hyperoperations-not their numeric values.

| PFN        | Structure                       | Knuth Arrows |
|------------|----------------------------------|---------------|
| `($1)`     | Single factorial                 | `↑`           |
| `($2)`     | B repetitions of `($1)`          | `↑↑`          |
| `($3)`     | B repetitions of `($2)`          | `↑↑↑`         |
| `($4)`     | B repetitions of `($3)`          | `↑↑↑↑`        |

> PFN replaces `^` with `!`, and turns repetition into **symbolic recursion**.

---

## 🚧 Future Enhancements

- 📊 Add visualizations for expansion trees (Fractal + Promotion)
- 🔍 Growth rate comparison against other large number notations (Conway, Ackermann)

---

## 👤 Contributors

- **Steve H.** — Creator and primary designer

---

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

---

> This documentation is a work in progress. Contributions, clarifications, examples, and visualizations are welcome!
