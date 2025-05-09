
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

### 🔄 Fully Lazy, Step-by-Step Solving

PFN is built as a **fully lazy, just-in-time system**. Nothing gets blown up all at once—every factorial, promotion, and dynamic placeholder stays dormant until it’s their turn to run.

#### 🔧 Valve-style execution  
Think of each symbol—`!`, `($n)`, `$dyn`, `>>`, `^`—as a **closed valve in a pipe**. You only “open” it when the flow of evaluation reaches that exact point.

#### 🔁 Base updates at every step  
After you solve a symbol (like a `!` or `($1)`), your **Base (B)** updates.  
The next promotion unfolds using **that new B**, not the one you started with.

#### 🚫 No bulk unpacking  
You never expand the whole chain of promotions at once. PFN **climbs the mountain one rung at a time**: solve a symbol → update context (base) → move on.

#### 🧰 On-demand macros  
Symbols like `($dyn)>>dyn` stay symbolic until they’re encountered.  
At that moment, `$dyn` reads the *current* B and expands just enough to keep climbing.

> This just-in-time magic is what lets PFN express **gargantuan growth** without calculating everything up front.

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



## 🌳 Part II: An Optional PFN fractal mode. AKA Fractorials (Fractal + Factorial)

“Fractorials” combine fractals and factorials: each number branches into smaller factorial chains, recursively, until all branches terminate on at 1. 

---

### 🧩 How It Works

Fractorials build a **factorial tree**, where each node greater than 1 creates its own subtree. The final result is the product of **all nodes** in the entire structure.

---

### 🔢 Fractal(4)

We’ll walk through the structure visually.

```
          4
         /
        3
       / \
      /   \
     2     2
    / \   / \
   1   1 1   1
```

- **4** has children: 3, 2, 1
- **3** creates its own subtree: 2, 1
- **2** creates: 1
- All leaf nodes = 1

Now multiply all nodes:
```
= 4 × 3 × 2 × 1 × 2 × 1 × 1 × 1 × 1
= 48
```

---

### 🔢 Fractal(5)

```       
                5
               /
              4
             / \
            /   \
           /     \
          /       \
         /         \
        3           3
       / \         / \
      /   \       /   \
     2     2     2     2
    / \   / \   / \   / \
   1   1 1   1 1   1 1   1
```

- Fractal(5) includes a duplication of the 4 => 3 => 2 => 1 trees 
- But **only one** copy of node 4.
- So we adjust by:

```
Fractal(5) = (Fractal(4)^2 × 5) / 4
           = (48^2 × 5) / 4
           = (2304 × 5) / 4
           = 2880
```

---

### 🧠 Why the Formula Works

**Formula:**
```
F(1) = 1  
F(n) = (F(n−1)^2 × n) / (n − 1)
```

- When building Fractal(n+1), the structure of Fractal(n) appears:
  - ✅ Once directly
  - ✅ Once nested under n+1
- This causes **double counting** of node `n`
- ✅ **Divide by (n−1)** to fix the for the shared node at 'n-1'
- ✅ **Multiply by (n+1)** to include new top-level node

---

### 🚀 Fractorial Growth

- Fractal(4) = 48  
- Fractal(5) = 2880  
- Fractal(6) = (2880^2 × 6) / 5 ≈ 9.9 million  
- Fractal(50) ≈ 10^29 digits  
- Fractal(2880) ≈ 10^(10^881)

Compared to Factorials:
- 4! = 24
- 5! = 120
- 6! = 720
- 50! ~ 3.04 × 10⁶⁴
---

> Fractorials explode in size due to **recursive self-similarity** and rapid compound branching.


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
3! = 6  
6! = 720  
720! ≈ 10^1340  
(720!)! ≈ 10^(1.34×10^1343)  
Next step: ≈ 10^(10^(1.34×10^1343))
```

So:
**3!!!!!!!! ≈ 10^(10^(1.34 × 10^1343))**

> Stirling's gives us usable approximations through **n₄** before all hell breaks loose.

---

## 🚀 Try It Yourself!

Start small: `3!($2)` → `3!!!!!!!`  
Build up: `4!($3)($4)($5)`  
Crank up the heat: `4!($3)($dyn)($dyn)`  
Go wild: `3!(($dyn)>>dyn)>>dyn` (repeats ($dyn)>>dyn) blocks, each lazily evaluated/solved when they are reached)

What’s the biggest number you can create succinctly?

---

## 👤 Contributors

- **Steve H.** — Creator and primary designer

---

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

---

> Contributions, diagrams, parsers, and recursive madness are welcome!
