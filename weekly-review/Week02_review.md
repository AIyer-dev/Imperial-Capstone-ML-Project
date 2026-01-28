# Week 2 Review – Adaptive Optimisation Strategy

This document captures the **Week 2 reflection** for the Black-Box Optimisation (BBO) capstone.  
Compared to Week 1, the focus shifted from generic probing to **function-specific, evidence-driven decision-making**.

---

## 1. Strategy Change from Week 1

In **Week 1**, the approach was primarily *first contact*. A Gaussian Process (GP) surrogate was fitted for each function using the limited initial data, and a standard acquisition function (Upper Confidence Bound or Expected Improvement) was applied uniformly across all functions. The goal was simply to obtain a reasonable first probe.

In **Week 2**, the strategy became **adaptive and function-specific** rather than uniform:

- **Promising functions (F4, F5, F7):** Shifted toward targeted local exploitation around the best-performing point observed so far.
- **Weak or unclear functions (F1, F3, F6):** Deliberately increased exploration to map previously unsampled regions.
- **High-dimensional function (F8):** Adopted a structured perturbation strategy rather than repeatedly sampling the same extreme corner.

This change was prompted directly by Week 1 outputs. For example, **F5 produced a very high value (~2523)**, strongly suggesting proximity to a good basin and justifying refinement. In contrast, **F1 and F6 returned near-zero or poor values**, indicating that a meaningful region had not yet been identified and that exploitation would be premature.

Overall, the shift was from **“one generic BO recipe”** to **“custom exploration–exploitation decisions per function.”**

---

## 2. Exploration vs Exploitation Trade-Offs

Both exploration and exploitation were used, but selectively.

### Exploitation-Focused Functions
- **F4 (4D)** and **F5 (4D)** delivered strong Week 1 results.
- Expected Improvement was used with a **very small ξ**, biasing the search toward incremental improvements near the current best.
- **Trade-off:** Risk of converging to a local maximum if the apparent optimum is not global.

### Exploration-Focused Functions
- **F1 (2D):** Output was effectively zero, so β was increased in UCB to prioritise uncertainty-driven exploration.
- **F3 (3D)** and **F6 (5D):** Continued poor performance justified sampling new regions.
- **F8 (8D):** A structured exploratory move was used by perturbing roughly half the coordinates away from 0.999999 to 0.8, testing sensitivity without random guessing.

The guiding principle was:  
> *Exploitation is valuable only after a promising region has been identified; otherwise, exploration is essential.*

---

## 3. Influence of Discussions and Outputs

Two main influences shaped the Week 2 approach:

1. **Flexibility in optimiser choice:** Class discussions emphasised that heuristic justification is acceptable. This encouraged tailoring acquisition functions per function rather than forcing Expected Improvement everywhere.
2. **Trust-region thinking:** Inspired by Bayesian optimisation in scientific domains (e.g. chemical yield tuning), strong results justified local perturbations instead of global sweeps. This was applied directly to **F5**, focusing on refining the high-yield neighbourhood.

Additionally, the Week 1 outputs themselves acted as empirical guidance. Large positive responses justified exploitation, while negative or flat responses justified broader exploration.

---

## 4. Linear / Logistic Regression Assumptions Likely Violated

Attempting to fit a simple linear regression to the current data would violate several assumptions:

- **Linearity:** Functions like **F5** are clearly nonlinear, exhibiting peaks rather than planar trends.
- **Additivity:** Strong interactions between dimensions are likely (e.g. one variable is beneficial only when others are high).
- **Homoscedasticity:** Some functions (e.g. F2, F3) appear noisier than others, violating constant-variance assumptions.
- **Sample size vs dimensionality:** For **F7 (6D)** and **F8 (8D)**, fitting even a linear model with so few samples would be statistically fragile and prone to overfitting.

---

## 5. Local Linearity and Logistic Regression as a Screening Tool

While global linearity is implausible, **local linear approximations** can still be informative.

- In **F5**, small perturbations around the high-performing point effectively explore a local trust region where monotonic behaviour may hold.
- Reframing the task as a **binary classification** (e.g. “good” vs “bad” output based on a threshold) could make logistic regression useful as a *screening tool*:
  - For **low-dimensional functions (e.g. F2)**, this could help identify a “hot zone.”
  - For **high-dimensional functions (F8)**, such classifiers would likely overfit due to extreme sparsity.

Thus, logistic regression would not solve optimisation directly, but could guide where exploitation is worthwhile in simpler cases.

---

## 6. Role of Interpretability in Query Selection

Interpretability played an important role despite not fitting explicit regression models.

- **F8 (8D):** Instead of resubmitting an “all ones” vector, a structured perturbation was used to assess which dimensions were truly critical.
- **F5 (4D):** Dimensions 3 and 4 were held fixed at 1.0 while dimensions 1 and 2 were adjusted, reflecting an implicit belief about feature importance.

This mirrors a regression-style mindset: *fix some variables, vary others, and observe marginal effects*. Such interpretability is crucial when only one query per function is allowed and decisions must be justified.

---

## Summary

- **Week 1:** Baseline BO per function.
- **Week 2:** Adaptive BO per function, with evidence-driven exploration vs exploitation.
- The strategy now incorporates **trust regions, sensitivity analysis, and interpretability**, moving beyond treating each function as an undifferentiated black box.

This marks a transition toward more mature, practitioner-style optimisation reasoning.
