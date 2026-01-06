# 📘 Bayesian Black-Box Optimisation (BBO) Capstone Project
*A multi-round optimisation challenge using Gaussian Processes and adaptive exploration strategies.*

## Additional Documentation
- [Datasheet](DATASHEET.md)
- [Model Card](MODEL_CARD.md)

## 1. Project Overview

This repository documents my work for the **Imperial College London BBO Capstone Project**, where the task is to optimise eight unknown (“black-box”) functions. Each function accepts continuous numerical inputs and returns a single scalar output, simulating real-world problems such as chemical yield optimisation, hyperparameter tuning, or industrial process control.

The overall objective is to **maximise** the output of each function using only a limited number of queries per week. The challenge is deliberately constrained:
- The function forms are unknown,
- Visualisations are not provided,
- Each evaluation is “expensive”,
- Only one query per function per week is allowed.

This mirrors real machine-learning and data-science environments where feedback is slow or costly (e.g., laboratory experiments, simulation-based engineering, or model hyperparameter search). Developing a principled optimisation strategy under uncertainty is highly transferable to real-world ML roles, especially in optimisation-heavy domains such as AutoML, reinforcement learning, experiment design, or applied analytics.

## 2. Inputs and Outputs

Each black-box function receives a **vector of continuous inputs** and returns a **single scalar performance value**.
- Functions range from **2D to 8D** (F1–F8 respectively).
- Inputs must be submitted in the exact format:
  ```
  0.xxxxxx-0.xxxxxx-...
  ```
  All values must begin with `0` and use six decimal places.

**Dimensions:**
- F1: 2D
- F2: 2D
- F3: 3D
- F4: 4D
- F5: 4D
- F6: 5D
- F7: 6D
- F8: 8D

**Outputs:**
Each function returns a real-valued number (positive, negative, or near zero). Higher values are better. Some functions may include noise or have multiple local optima.

**Constraints and Limitations:**
- One query per function per week.
- No access to the underlying equation or gradient.
- Outputs arrive with delay, requiring iterative planning.
- Query format strictly enforces the “0.xxxxxx” rule.

## 3. Challenge Objectives

The primary goal is to **maximise** all eight functions using a principled sequence of queries. Because the underlying functions are unknown, the project tests my ability to:

- Build surrogate models from limited data,
- Manage the trade-off between exploration and exploitation,
- Adapt strategies as evidence accumulates,
- Justify decisions under uncertainty,
- Communicate ML reasoning clearly.

Constraints include the **small dataset size**, the **black-box structure**, and the inability to perform batch evaluations — all of which make classical grid search or brute force approaches infeasible.

## 4. Technical Approach

### **Week 1 → Initial Exploration**
I began with the 10 initial (x, y) points provided for each function. I fitted **Gaussian Process (GP)** surrogate models, using kernels suited for moderate smoothness.
- Acquisition functions: **UCB** for exploration and **EI** for early exploitation.
- Strategy: Broad exploration across the input space to learn the global structure.

### **Week 2 → Adaptive Per-Function Strategy**
After receiving the first round of outputs, the strategy diverged by function:

- **High-potential regions (F2, F4, F5, F7):** Adopted **local exploitation** using EI with low ξ to refine good zones.
- **Flat or uncertain functions (F1):** Increased exploration (higher β in UCB).
- **Noisy or ambiguous functions (F3, F6):** Used a mix of local and global probing.

This reflects standard BO behaviour: as uncertainty decreases, the model shifts toward exploitation.

### **Week 3 → Structured Refinement**
By the third round, several functions showed stable patterns. I used **trust-region style perturbations** around high-performing areas to identify gradients:

- **F5 and F8:** Strong improvements guided small perturbations near known optima.
- **F7:** Demonstrated monotonic trends in some dimensions, prompting targeted refinement.
- **F6:** Local improvements suggested moderate exploration around the Week-2 success.
- **F1:** Still flat → continued exploration.

At this stage, decisions relied more on model-informed reasoning and less on broad-space heuristics.

### **ML Methods and Considerations**
- **Gaussian Processes** for regression and uncertainty estimation.
- **UCB and EI acquisition functions**, tuned conceptually rather than by hyperparameter search.
- Consideration of **SVMs and logistic regression** as alternative approaches:
  - A soft-margin SVM could separate “high” vs “low” performing regions.
  - Kernel SVMs would capture non-linear boundaries.
  - However, they lack the uncertainty quantification essential to BO.

### **Exploration vs Exploitation**
My approach balances exploration early on where structure is unknown, then shifts toward exploitation as high-value basins emerge. The strategy is unique per function rather than uniform across all eight.

### **Week 4 → Early Exploitation and Pattern Confirmation**
By Week 4, several functions began to show repeatable structure rather than random variation. The strategy shifted toward **confirming promising regions** rather than discovering new ones.

- **F2, F4:** Clear ridge / basin behaviour emerged, so queries focused on refining these areas with small directional steps.
- **F5:** Strong monotonic improvement suggested a smooth gradient; exploitation was prioritised.
- **F8:** Early signs of a plateau led to symmetry-based probing around the apparent optimum.
- **F1:** Continued to show no signal, reinforcing its low priority.

This week marked the transition from global exploration to function-specific optimisation.

### **Week 5 → Trust-Region Optimisation**
In Week 5, I adopted an explicit **trust-region mindset**. Instead of moving broadly, I made small, interpretable perturbations around the best-known points for each function.

- Exploitation dominated for **F5, F6, F7**, where gradients appeared reliable.
- **F4** required corrective steps after overshooting, highlighting narrow optima.
- **F3** was refined cautiously due to noisy behaviour.

This reduced variance and improved interpretability of results.

### **Week 6 → Convergence Signals and Stability Checks**
Week 6 focused on distinguishing **true convergence from temporary improvements**.

- **F8** repeatedly returned the same maximum value, indicating a stable plateau.
- **F5** continued improving, justifying further exploitation.
- **F6** showed signs of approaching an optimum but with increasing sensitivity.
- **F1** was effectively deprioritised.

At this point, exploration was only used where uncertainty remained justified.

### **Week 7 → Late-Stage Refinement**
By Week 7, optimisation became increasingly conservative.

- Small asymmetric perturbations were used to test whether optima were perfectly symmetric or slightly skewed.
- Several functions (notably **F2, F4, F7**) were refined with minimal step sizes.
- Performance stability became as important as raw improvement.

This mirrors real-world optimisation, where robustness often outweighs marginal gains.

### **Week 8 → Selective Investment**
Week 8 introduced **selective optimisation**, where effort was concentrated only on functions that still showed meaningful returns.

- **F5** remained the primary optimisation target due to continued monotonic gains.
- **F3 and F4** were refined cautiously.
- **F1 and F8** were effectively frozen to conserve budget.

This prevented wasted queries on flat or converged objectives.

### **Week 9 → Pre-Convergence Strategy**
By Week 9, the strategy clearly reflected a **pre-convergence phase**.

- Most functions were operating within narrow trust regions.
- Corrections were made where overshooting occurred (notably **F6**).
- Emphasis shifted toward reproducibility and stability rather than aggressive search.

This stage prioritised defensible optimisation decisions over speculative exploration.

### **Week 10 → Consolidation and Risk Management**
Week 10 focused on consolidating gains while managing late-stage risk.

- **F5** continued to receive controlled exploitation.
- **F2, F3, F4, F7** were adjusted only marginally to avoid destabilisation.
- **F1 and F8** were treated as converged.

By this point, optimisation had transitioned from discovery to **management**, reflecting the realities of optimisation under strict computational constraints.

