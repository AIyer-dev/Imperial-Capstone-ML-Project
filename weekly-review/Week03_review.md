# Week 3 Review – Exploitation-Leaning Optimisation Strategy

This document captures the **Week 3 strategy reflection** for the Black-Box Optimisation (BBO) capstone, written **before receiving Week 3 outputs**.  
By this stage, sufficient evidence had accumulated to justify a shift toward **local refinement and trust-region optimisation** for most functions.

---

## 1. Strategy Change from Week 2

In **Week 2**, the strategy remained mixed: some functions were explored broadly, while others began transitioning toward refinement.  
By **Week 3**, the approach became noticeably more **exploitation-leaning** for functions where early structure had emerged.

Specifically:

- **Exploitation-focused functions:**  
  **F3, F4, F5, F6, F7, F8** all showed identifiable higher-performing regions in Weeks 1–2. This justified trust-region style local refinement around the strongest known points.
- **Exploration-focused function:**  
  **F1** continued to exhibit near-flat behaviour, so an exploratory strategy was maintained.
- **Structured exploitation along a boundary:**  
  **F2** showed a clear high-value ridge near the upper boundary (*x₂ ≈ 1*), prompting focused exploitation along this ridge.

This shift was prompted by the increasing confidence of the surrogate model. As more data accumulated, the posterior mean became informative enough that broad exploration delivered diminishing returns. At this stage, Bayesian Optimisation naturally transitions toward exploitation.

---

## 2. Exploration vs Exploitation Trade-Offs

Week 3 was **predominantly exploitation-oriented**, but with controlled, low-risk exploration where uncertainty remained.

### Exploitation-Dominant Functions
- **F2, F3, F4, F5, F6, F7, F8**

For these functions, small structured perturbations around high-performing points were used rather than large jumps. This aligns with Expected Improvement using a small ξ, where the goal is incremental improvement rather than discovery.

### Exploration-Dominant Function
- **F1**

After two rounds of near-zero outputs, exploitation offered no meaningful benefit. High-uncertainty exploration remained the only rational strategy.

### Trade-Offs Considered
- Exploiting too early risks local optima, but this risk is low for smoother or unimodal functions (e.g. F5).
- Excessive exploration in later weeks wastes scarce evaluations, especially in high-dimensional spaces (F7, F8).
- The objective is not perfect optimisation but **adaptive, evidence-driven reasoning**, which requires different strategies per function.

---

## 3. Influence of Discussions and Prior Outputs

Week 3 decisions were shaped by both course content and empirical evidence:

- Course material emphasised that BO gradually shifts from exploration to exploitation as confidence grows.
- For **F8**, discussions on the difficulty of high-dimensional search motivated structured perturbations rather than random exploration.
- Observations from Week 2 were particularly influential:
  - **F5:** A performance drop after moving away from the Week 1 optimum suggested the need to return to local refinement.
  - **F7:** Strong improvement in Week 2 justified continued exploitation.
  - **F6:** Improvement after leaving the Week 1 region justified micro-exploration in that direction.

---

## 4. Linear / Logistic Regression Assumptions Likely Violated

For most functions (notably **F3, F6, F7, F8**), fitting a simple linear or logistic regression would violate key assumptions:

- **Non-linearity:**  
  Outputs show curvature and sensitivity peaks inconsistent with linear relationships (e.g. F5’s sharp optimum, F8’s complex surface).
- **Additivity:**  
  Strong feature interactions are likely, especially in hyperparameter-style functions.
- **Homoscedasticity:**  
  Noise appears region-dependent in several functions.
- **Sample size vs dimensionality:**  
  Extremely sparse sampling in 6D–8D spaces would cause severe overfitting.

As a result, linear or logistic models would misrepresent the true structure.

---

## 5. Local Linearity and Logistic Regression as a Boundary Tool

Although global linearity is implausible, **local approximations** can still be informative:

- **F5:** Near the Week 1 optimum, the surface behaves almost like a sloped plane until reaching the peak.
- **F2:** Exhibits threshold-like behaviour near *x₂ ≈ 1.0*. A logistic classifier on “high vs low output” could identify this boundary.

However, such models would:
- Fail globally due to curvature,
- Overfit in high dimensions,
- Provide only coarse guidance.

Still, boundary thinking was useful, particularly in justifying continued focus near *x₂ ≈ 1* for F2.

---

## 6. Role of Interpretability in Decision-Making

Interpretability increasingly guided Week 3 decisions, especially in higher dimensions:

- **F8:** Reducing dimensions 1–4 from 1.0 to 0.8 in Week 2 improved performance, indicating non-monotonic feature effects. Week 3 explored this region further (≈0.75–0.85).
- **F7:** Dimension 1 consistently favoured values near 0.0, a stable interpretable pattern preserved in Week 3.
- **F5:** Dimensions 3 and 4 strongly preferred the upper boundary. These were fixed while dimensions 1–2 were refined.

This feature-effect mindset mirrors how practitioners tune scientific processes or ML systems: fix known-critical variables and adjust uncertain ones.

---

## Summary

Week 3 marks a clear maturation of the optimisation strategy:

- Increased exploitation where evidence supports it,
- Continued exploration where information remains weak,
- Trust-region refinement around discovered optima,
- Awareness of dimensional sensitivity and feature roles,
- A more practitioner-like, data-driven BO mindset.

This week represents a transition from exploratory optimisation to **controlled convergence**.

---
