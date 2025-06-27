# Advanced-Machine-Learning

# Probabilistic Graphical Models - Week 1 Theory Notes

Welcome to the comprehensive documentation on **Probabilistic Graphical Models** (PGMs) based on Week 1 theory sessions. This repo explains the foundational concepts of **Bayesian Networks (BNs)**, **Undirected Graphical Models (UGMs)**, and **Inference Algorithms** in PGMs.

---

## 📘 Contents

1. [Bayesian Networks (BN)](#bayesian-networks-bn)
2. [Undirected Graphical Models (UGM)](#undirected-graphical-models-ugm)
3. [Inference in PGMs](#inference-in-pgms)

---

## Bayesian Networks (BN)

### 🧠 Key Concepts

- **Directed Acyclic Graphs (DAGs)** where each node represents a random variable.
- Each node has a conditional probability distribution (CPD) given its parents.
  
### 🔢 Factorization

The joint probability over N variables:
```
P(x₁, ..., xN) = ∏ Pr(xᵢ | Parents(xᵢ))
```

### 📌 Conditional Independencies (CI)

- **Local CI**: A variable is independent of its non-descendants given its parents.
- **Global CI**: Determined using **d-separation**.

### 🛠 Building a BN from CI Queries

Algorithm (given access to CI queries):
1. Choose variable ordering.
2. For each variable, find minimal set `S` of earlier variables such that:
   ```
   xi ⊥⊥ rest | S
   ```
3. Make all nodes in `S` parents of `xi`.

### 🔁 Equivalence of BNs

Two BNs are equivalent if they have:
- The same skeleton (underlying undirected graph).
- The same immoralities (v-structures like `A → C ← B` without a direct edge between A and B).

### ❌ Limitations

BNs **cannot** represent:
- Symmetric relationships.
- Certain dependency structures, e.g., `{X ⊥⊥ Y}, {X ⊥⊥ Z}, {Y ⊥⊥ Z}, {X ⊥̸⊥ {Y,Z}}`.

---

## Undirected Graphical Models (UGM)

### 📌 Definition

- Graph is undirected.
- Nodes are variables, edges imply potential relationships.
- Used in scenarios where **symmetry** is important (e.g., image pixels, social networks).

### 🧮 Factorization

The joint probability:
```
P(x₁, ..., xN) = (1/Z) ∏ ψ_C(x_C)
```
Where:
- ψ_C are **potentials** over cliques.
- `Z` is the **partition function** ensuring normalization.

### 🔍 Global Conditional Independence

Use **graph separation**:
- `X ⊥⊥ Y | Z` ⇔ Z separates X and Y in the graph.

### 🛠 Constructing UGMs

1. **From factors**: Connect variables in the same factor.
2. **From CI queries**:
   - Add edge between xi, xj if they are not conditionally independent given all others.

### 🧱 Markov Blanket in UGMs

For node `xi`, Markov blanket is its set of neighbors:
```
xi ⊥⊥ rest | neighbors(xi)
```

### 📏 Hammersley-Clifford Theorem

For **positive distributions**, factorization over cliques ⇔ global CI structure.

### 🔁 Conversion Between BN and UGM

- **BN → UGM**: Use **moralization**: connect parents of a node, drop direction.
- **UGM → BN**: Only possible for **chordal (triangulated)** graphs.

---

## Inference in PGMs

### 🔍 Types of Inference

1. **Marginal Inference**: Compute P(Xᵢ | evidence)
2. **MAP Inference**: Find x* that maximizes P(x | evidence)

### 🧱 Variable Elimination (VE)

- Exact inference algorithm.
- Iteratively eliminate variables by marginalizing.

```python
Z = ∑_x₁ ∑_x₂ ... ∑_xn ∏ ψ(x_C)
```

### 📉 Complexity

- VE is exponential in treewidth.
- Optimal elimination order is **NP-hard** to find.

### 🔁 Approximate Inference Methods

- **Sampling**: MCMC, Gibbs Sampling.
- **Variational Inference**: Approximate P with a simpler Q.
- **Loopy Belief Propagation**: Iterative message-passing even in cyclic graphs.

### 🔀 Junction Tree Algorithm

1. Triangulate graph.
2. Build **clique tree**.
3. Use **message passing** for efficient inference.

### 🔄 Belief Propagation (BP)

- Messages sent from variables to factors and back.
- Two-pass (upward and downward).
- Efficient on tree-structured graphs.

### 🧮 Baum-Welch (Sum-Product in Chains)

- Special case for **HMMs**.
- Efficient forward-backward computation of marginals.

---

## 📚 Summary

| Property                  | BN                           | UGM                         |
|--------------------------|------------------------------|-----------------------------|
| Graph Type               | Directed (DAG)               | Undirected                  |
| Independence Criteria    | d-separation                 | Graph separation            |
| Factorization            | CPDs (local)                 | Cliques (global)            |
| Symmetric Dependencies   | Not well-handled             | Naturally handled           |
| Conversion               | Via moralization (BN→UGM)    | Requires chordal graph (UGM→BN) |
| Efficient Inference      | VE, Junction Tree, Sampling  | VE, Belief Propagation      |

---

## 📌 References

- Kevin Murphy's book: *Machine Learning: A Probabilistic Perspective*
- Daphne Koller & Nir Friedman: *Probabilistic Graphical Models*
- Week 1 PDFs: BN, UGM, Inference (see `/pdfs/` folder)

---

## 📁 Files

- `Week-1 Theory 1.pdf`: Bayesian Networks
- `Week-1 Theory-2.pdf`: Undirected Graphical Models
- `Week-1 Theory-3.pdf`: Inference in PGMs

Feel free to open issues or contribute improvements! 🚀

---

