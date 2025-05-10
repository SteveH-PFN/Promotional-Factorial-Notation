## **Factorial Fractals**

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


Compared to Factorials:
- 4! = 24
- 5! = 120
- 6! = 720
- 50! ~ 3.04 × 10⁶⁴

---

> Fractorials explode in size due to **recursive self-similarity** and rapid compound branching.

---

### 📈 Logarithmic Growth Insight

As `n` increases, the base-10 logarithm of Fractal(n) **asymptotically doubles** at each step:

```
log₁₀(F(n+1)) ≈ 2 × log₁₀(F(n))
```

This results in **exponential growth of exponential growth**, overtaking standard factorials dramatically.

### Promotional Factorial Notation

I stumbled on Fractorials when contemplating another notation, PFN, which uses recursion and step-by-step evaluation to create large number. You can read more here:
[View the PFN page here](https://github.com/SteveH-PFN/Promotional-Factorial-Notation/edit/main/README.md)
