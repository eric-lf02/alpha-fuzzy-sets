# 🔢 Fuzzy Sets Lab

A Python implementation of alpha-cut fuzzy sets with support for union, intersection, addition, and multiplication operations, developed as a laboratory project for a **Fuzzy Systems and Evolutionary Computing** course.

---

## Overview

This project extends the [softpy](https://pypi.org/project/softpy/) library by introducing two new classes built on top of `ContinuousFuzzySet`:

- **`AlphaFuzzySet`** — represents a fuzzy set defined by a dictionary of α-cuts, where each key is an alpha level and each value is a list of intervals
- **`AlphaFuzzyCombination`** — combines two `AlphaFuzzySet` instances using a continuous associative function, leveraging the property that for any continuous function **f: ℝ² → ℝ**:

> ∀α ∈ [0,1], [f(F₁, F₂)]ₐ = f([F₁]ₐ, [F₂]ₐ)

---

## What Are Alpha Cuts?

Alpha cuts (α-cuts) are a fundamental tool in fuzzy set theory. An α-cut of a fuzzy set includes all elements whose membership degree is **greater than or equal to α**. They allow fuzzy sets to be represented as families of crisp (classical) sets, one for each level α ∈ [0,1].

---

## Features

### `AlphaFuzzySet`
- Defined by a dictionary mapping alpha levels to lists of intervals
- Validates proper nesting of α-cuts (higher alpha intervals must be subsets of lower alpha intervals)
- Supports:
  - `__call__(x)` — returns the membership degree of `x`
  - `__getitem__(alpha)` — returns the α-cut for a given alpha level
  - `fuzziness()` — computes the fuzziness of the set
  - `hartley()` — computes the Hartley entropy of the set

### `AlphaFuzzyCombination`
Combines two `AlphaFuzzySet` instances using one of four operations:

| Operation | Description |
|-----------|-------------|
| `union` | μ_C(x) = max(μ_A(x), μ_B(x)) |
| `intersection` | μ_C(x) = min(μ_A(x), μ_B(x)) |
| `addition` | Minkowski sum of the α-cut intervals |
| `multiplication` | Interval multiplication of the α-cut intervals |

---

## Running

The notebook is hosted on Google Colab — no local setup required.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1CTkjX6Jbe-eER44ngBliWt3T6yuxVAGF)

To run it locally instead:

```bash
pip install softpy numpy scipy matplotlib
jupyter notebook fuzzyproject.ipynb
```

---

## Notebook Structure

The notebook is divided into two main parts:

**Part 1 — AlphaFuzzySet**
- Definition and validation of fuzzy sets via α-cuts
- Computation of membership degree, fuzziness, and Hartley entropy
- Plotting of fuzzy sets

**Part 2 — AlphaFuzzyCombination**
- Combination of two fuzzy sets via union, intersection, addition, and multiplication
- Graphical visualization of each combined result

---

## Example

```python
fuzzy_set1 = AlphaFuzzySet({
    0.6: [(3, 3)],
    0.4: [(2, 4)],
    0.2: [(1, 5)],
    0.0: [(0, 6)]
})

fuzzy_set2 = AlphaFuzzySet({
    1.0: [(2, 3)],
    0.8: [(1.5, 3.5)],
    0.6: [(1, 4)],
    0.4: [(0.5, 4.5)],
    0.2: [(0, 5)],
    0.0: [(0, 6)]
})

combined_union         = AlphaFuzzyCombination(fuzzy_set1, fuzzy_set2, 'union')
combined_intersection  = AlphaFuzzyCombination(fuzzy_set1, fuzzy_set2, 'intersection')
combined_addition      = AlphaFuzzyCombination(fuzzy_set1, fuzzy_set2, 'addition')
combined_multiplication = AlphaFuzzyCombination(fuzzy_set1, fuzzy_set2, 'multiplication')
```


## License

MIT
