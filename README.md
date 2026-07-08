# Formalization of Hilbert Spaces and the Riesz Representation Theorem in Lean 4

**Bachelor's Thesis — BSc in Mathematics, University of Seville (2024)**

This project formalizes the basic theory of Hilbert spaces in the **Lean 4** proof assistant, culminating in a computer-verified proof of the **Riesz representation theorem**: every bounded linear functional on a Hilbert space can be uniquely represented as an inner product.

## What does it mean to "formalize" a theorem?

Formalizing mathematics means writing definitions and proofs in a language that a computer can **verify step by step**. Unlike a pen-and-paper proof, there are no gaps and no "left as an exercise": every logical step must be justified all the way down to the axioms, and the proof assistant (Lean) mechanically checks that everything is correct. If the code compiles, the proof is valid.

This kind of work demands a deep command of both the underlying mathematics and rigorous logical reasoning, and it is the foundation of projects like [Mathlib](https://github.com/leanprover-community/mathlib4), the largest library of formalized mathematics in the world, whose style and tooling this project follows.

## What is formalized

Starting almost from scratch (defining the structures rather than importing them ready-made), the development builds:

1. **Inner product spaces** — the `InnerProductSpace` class, with the inner product and its axioms (positivity, conjugate symmetry, linearity).
2. **Induced norm and metric** — the norm defined from the inner product, together with proofs of its properties.
3. **Cauchy-Schwarz inequality** — the key ingredient for proving that the induced norm is indeed a norm.
4. **Completeness and Hilbert spaces** — Cauchy sequences, convergence, and the `HilbertSpace` class as a complete inner product space.
5. **Riesz representation theorem** — the main result, in two parts:
   - *Existence*: every bounded linear functional `f : F → 𝕜` is represented as `f(x) = ⟨x, z⟩` for some `z`, building on the orthogonal projection theorem.
   - *Uniqueness*: the representing vector `z` is unique (`unicidad_riesz`).

## Repository structure

```
EspaciosHilbert/
├── definiciones.lean     # Inner product, inner product spaces, completeness, Hilbert spaces
├── lemas.lean            # Auxiliary lemmas about the inner product
├── cauchyschwarz.lean    # Cauchy-Schwarz inequality
├── normainducida.lean    # The induced norm and its properties
├── metricainducida.lean  # The metric induced by the norm
└── riesz.lean            # Orthogonal projection and the Riesz representation theorem
```

In total, ~650 lines of Lean 4 organized as modules: each file imports the previous ones, mirroring the layered mathematical construction.

## Technical details

- **Lean 4** (`v4.7.0-rc2`) with the **Lake** build system.
- Dependencies: **Mathlib 4** (base types such as `IsROrC` to work over ℝ and ℂ in a unified way) and **Aesop**.
- The main structures (`Inner`, `InnerProductSpace`, `HilbertSpace`) are defined within the project itself following Mathlib's style, instead of reusing the library's versions — the goal of the thesis was to build the theory, not to consume it.
- The orthogonal projection theorem onto the kernel of the functional is introduced as an axiom (`teorema_proyeccion`); from it, the orthogonality of the projection, the existence of the Riesz representative and its uniqueness are proved.
- Proofs are written in Lean 4 tactic mode (`by_contra`, `push_neg`, `obtain`, rewriting with `rw`, etc.).

## Building

With [elan](https://github.com/leanprover/elan) installed (it manages the Lean version automatically via `lean-toolchain`):

```bash
lake update      # downloads Mathlib and Aesop
lake build
```

> Note: the first Mathlib build can take a long time; `lake exe cache get` downloads precompiled binaries and speeds it up considerably.

## Context

This repository contains the Lean 4 development of my Bachelor's Thesis, *"Formalization of Hilbert Spaces in Lean4"* (BSc in Mathematics, University of Seville). The written thesis develops the mathematical theory alongside the code. Source files and identifiers are named in Spanish, matching the thesis.

---

*Author: Adrián García Ruiz — [github.com/AdrianGR517](https://github.com/AdrianGR517)*
