
# Promotional Factorial Notation (PFN)

**A large number notation system based on factorials and recursive operations**  
Developed by **Steve H.** (2025)  
Licensed under the MIT License

---

## 🧠 TL;DR

**PFN builds absurdly huge numbers using symbolic factorial macros instead of arrows.**  
Example: `3!($2)` → `3! = 6`, so inject 6 `($1)` → `3!!!!!!!` (6 factorials deep).  
PFN notation removes the need for parenthesis in iterated factorials, so 3!!! = ((3!)!)!

---

## 🌟 Quick Example


### 🔍 Basic example: `3!($3)` → B = 6

```
3!($3)                                                      # Factorials expanded, others remain
→ 3!($2)($2)($2)($2)($2)($2)                                # ($3) changes into B=6 number of ($2)
→ 3!($1)($1)($1)($1)($1)($1)($2)($2)($2)($2)($2)            # One ($2) expands into B number of ($1) 
→ 3!!!!!!!($2)($2)($2)($2)($2)                              # The next ($2) becomes 3!!!!!!! number of ($1)
```


**Final form:**  
`3!($1)^6 ($2)^5 ($3)^5`

**Notes:**
- No bulk operations can define what a ($n) will be at the time they are expanded to the lower level. PFN solves one step at a time.
- ($1) is the same thing as adding a factorial to the expression. 3!($1) → 3!! → 6! → 720
---

## 📘 Overview

Promotional Factorial Notation (PFN) reimagines factorial chaining in a symbolic language of recursive growth.  
Instead of using hyperoperations like Knuth's up-arrows, PFN builds massive values using layered factorials and recursive macros called **promotion levels**.

With **Fractal Mode** (AKA Fractorials), PFN achieves structurally recursive number growth that takes it to the next level. 

---

## 🧮 Core Symbols

| Symbol         | Description                                                          |
|----------------|----------------------------------------------------------------------|
| `!, ($1)`      | Standard factorial                                                   |
| `!!, !!!`      | Chained factorials (left to right)                                   |
| `($n)`         | Promotion level: expands into B copies of ($n−1)                     |
| `$dyn`         | Dynamic placeholder: resolves to current B at evaluation             |
| `^`            | Repeat previous symbol a number of times (e.g., `($1)^6`)            |
| `>>`           | Repeat previous block                                                |

Start with `!`, `($n)`. Save `$dyn`, `^`, and `>>` for later.

---

## 🔧 Base Mechanics

### 🧱 Base (B)

- PFN begins with a whole number and optional factorials:
  - `3! = 6`
  - `3!! = 6! = 720`
- This result becomes the **Base (B)** for promotion evaluations. **B** is not static through unsolved PFN expressions. It will change as you solve the expression. 

### 🪜 Promotions

| Symbol   | Meaning                           |
|----------|-----------------------------------|
| `($1)`   | Apply one factorial (!)           |
| `($2)`   | B copies of `($1)`                |
| `($3)`   | B copies of `($2)`                |

> Each `($n)` expands into lower promotions **using the current B value**.

---

## 🔄 Dynamic `$dyn`

- `$dyn` evaluates to current B **at the moment it is read**.
- Used **after** static promotions.

Example:  
`3!!($dyn)`  
→ `3!! = 720` → `$dyn = ($720)` → `3!!($720)`

With repetition:  
`3!($dyn)>>5` → inserts 5 copies of `($dyn)`
→ 3!($dyn)($dyn)($dyn)($dyn)($dyn)
 
---

## ✅ Valid Syntax

- Promotions must be **ascending**
- `$dyn` must follow all static symbols

✅ Valid: `3!($2)($3)($4)`  
❌ Invalid: `3!($4)($2)`, `($3)3!`, `3!($dyn)($2)`

PFN expressions rewrite in ascending order every step of the sequence. 

---

## 🔍 First Simplified Form

B!($L) ≈ B! · ($1)^B · ($2 → $L−1)^(B−1)


### 🔍 Worked Example: `3!($4)` → B = 6

```
3!($4)
→ 3!($3)($3)($3)($3)($3)($3)                                                    # ($4) becomes 6 copies of ($3)
→ 3!($2)($2)($2)($2)($2)($2)($3)($3)($3)($3)($3)                                # One ($3) becomes 6 copies of ($2)
→ 3!($1)($1)($1)($1)($1)($1)($2)($2)($2)($2)($2)($3)($3)($3)($3)($3)            # One ($2) becomes 6 copies of ($1)
     
           
→ 3!!!!!!!($2)^5($3)^5            # Factorials expanded, others remain
```

**Final form:**  
`3!($1)^6 ($2)^5 ($3)^5`

## 📦 Bulk Notation

Compress long repeated chains.

### Basic Format:
`(n: $symbol)` → n copies of promotion

**Example:** `3!(6: $1)` = `3!($1)^6` = `3!!!!!!!`

### Range Format:
`(n: $2, $3)` = repeat both symbols n times  
`(5: $2 → $4)` = $2, $3, $4 ×5

### Valid:
- `3!(6:$1)(5:$2, $3)`  
- `3!(range $2-$5)^B`

❌ Invalid:
- `3!(5:$4, $2)` (not ascending)  
- `3!(($1)^6, ($1)^6)` (duplicated)

---

## 🔁 PFN vs. Hyperoperations

| PFN        | Structure                        | Knuth Arrows |
|------------|----------------------------------|--------------|
| `($1)`     | Single factorial                 | ↑            |
| `($2)`     | B × `($1)`                       | ↑↑           |
| `($3)`     | B × `($2)`                       | ↑↑↑          |

> PFN swaps exponentiation with **symbolic recursion**. Structural similarity doesn't lead to as large of values for small PFN expressions.

---

## 📈 3!!!!!!!! - Stirling Breakdown

7 chained factorials:

```
3!       = 6
3!!      = 720
3!!!     = 10^1746.415
3!!!!    = 10^(1.746×10^1749)
3!!!!!   = 10^(10^(1.746×10^1749))
3!!!!!!  = 10^(10^(10^(1.746×10^1749)))
3!!!!!!! = 10^(10^(10^(10^(1.746×10^1749))))
```

So:
**3!!!!!!!! ≈ 10^(10^(10^(10^(1.746×10^1749))))**

> Stirling's gives us usable approximations.

---

## 🚀 Try It Yourself!

Start small: `3!($2)` → `3!!!!!!!`  
Build up: `4!($3)($4)($5)`  
Crank up the heat: `4!($3)($dyn)($dyn)`  
Go wild: `3!(($dyn)>>dyn)>>dyn` (repeats ($dyn)>>dyn) blocks, each lazily evaluated/solved when they are reached)

What’s the biggest number you can create succinctly?

---


## 🌳 Optional DLC or stand-alone: Fractal Factorials (Fractorials, if you're feeling cheeky)

“Fractorials” combine fractals and factorials: each number branches into smaller factorial chains, recursively, until all branches terminate on at 1. 

[View the Factorial Fractals page here](https://github.com/SteveH-PFN/Promotional-Factorial-Notation/blob/main/Factorial%20Fractals.md)


## 👤 Contributors

- **Steve H.** — Creator and primary designer

---

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

---

> Contributions, diagrams, parsers, and recursive madness are welcome!
