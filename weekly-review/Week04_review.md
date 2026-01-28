# Week 4 Review – Trust-Region Refinement and Controlled Rollback

This document captures the **Week 4 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By this stage, the optimisation process had clearly moved into a **trust-region refinement phase**, with most functions showing identifiable basins or ridges.

---

## 1. Overall Strategy in Week 4

Compared to Week 3, the Week 4 strategy was **less about discovering new structure** and more about **confirming and refining** previously identified promising regions.

- For most functions, evidence from Weeks 1–3 indicated that good basins had already been located.
- As a result, Week 4 prioritised **local exploitation with cautious micro-exploration** rather than global search.
- The one exception remained **F1**, which continued to show no structure and therefore justified continued exploration.

This reflects a natural Bayesian Optimisation progression: as posterior confidence increases, the value of broad exploration diminishes and trust-region refinement becomes optimal.

---

## 2. Function-by-Function Rationale

### **F1 (2D – Flat, No Structure Yet)**
**Submitted:** `0.900000-0.100000`

All outputs from Weeks 1–3 remained effectively zero, with no discernible trend. This indicates either an extremely flat function or a very narrow optimum that has not yet been discovered.  
Exploitation is therefore meaningless. Week 4 continued **pure exploration**, deliberately jumping to a very different corner of the space (high x₁, low x₂) to test for any non-trivial response.

---

### **F2 (2D – Ridge Near x₂ ≈ 1)**
**Submitted:** `0.690000-0.999999`

- Week 1 near `(0.70, 1.0)` produced the best result so far.
- Weeks 2–3 perturbations away from this point reduced performance.

This strongly suggests a local optimum along a ridge near *x₂ ≈ 1*. Week 4 applied **fine-grained exploitation**, nudging *x₁* slightly left while keeping *x₂* fixed at its empirically optimal boundary. This is a textbook Expected Improvement step along a ridge.

---

### **F3 (3D – Basin Near High Corner)**
**Submitted:** `0.950000-0.600000-0.900000`

The strongest results continued to cluster near the Week 1 region. Week 3 improvements did not surpass that early configuration, indicating a stable basin.  
Week 4 therefore revisited the same region with a **directional perturbation**: holding *x₁* high, slightly lowering *x₂*, and increasing *x₃* to test whether the optimum extends further along that axis.

---

### **F4 (4D – Warehouse Placement, New Best in Week 3)**
**Submitted:** `0.440000-0.340000-0.380000-0.380000`

Week 3 produced a new best result, overtaking earlier rounds. This strongly indicated a good local basin.  
Week 4 continued **trust-region refinement**, making small, systematic shifts around the Week 3 configuration to probe for a local peak without risking a large regression.

---

### **F5 (4D – Chemical Yield, Unimodal Behaviour)**
**Submitted:** `0.220000-0.850000-0.999999-0.999999`

F5 has consistently behaved like a smooth unimodal surface:

- Week 1: strong yield,
- Week 2: moving away reduced performance,
- Week 3: local refinement improved yield further.

Week 4 followed a classic laboratory-style optimisation strategy: **keep critical parameters fixed** (dims 3 and 4 at 0.999999) and **incrementally adjust the remaining dimensions** to continue climbing the peak.

---

### **F6 (5D – Recipe Score, Gradual Improvement)**
**Submitted:** `0.350000-0.300000-0.400000-0.880000-0.070000`

Although outputs remain negative by design, Weeks 1–3 showed steady improvement as the search moved away from the initial configuration.  
Week 4 continued local refinement around the best-known region, applying small increases in the most sensitive dimensions and a slight decrease where prior evidence suggested diminishing returns. This is an exploitation-leaning move with built-in micro-exploration.

---

### **F7 (6D – Hyperparameters, Rollback Toward Best)**
**Submitted:** `0.000000-0.460000-0.245000-0.170000-0.395000-0.680000`

- Week 2 delivered the best F7 value so far.
- Week 3 overshot slightly and performed worse.

This suggests the true optimum lies closer to the Week 2 configuration. Week 4 therefore **interpolated between Week 2 and Week 3**, biasing toward the better-performing point. This cautious rollback mirrors how hyperparameter tuning is performed in practice: gradual correction rather than drastic jumps.

---

### **F8 (8D – High-Dimensional Basin Around 0.8–0.85)**
**Submitted:**  
`0.820000-0.780000-0.820000-0.780000-0.999999-0.999999-0.999999-0.999999`

Evidence from Weeks 1–3 indicated a strong basin when the first four dimensions lie around 0.8–0.85, with the remaining dimensions maximised.  
Week 4 refined within this basin by selecting intermediate values between the best-performing earlier points, while keeping dims 5–8 fixed. This reflects best practice in high-dimensional BO: **stay in the valley, probe gently along a few axes**.

---

## Summary

Week 4 represents a clear consolidation phase:

- **F1:** Continued exploration due to lack of structure.
- **F2–F8:** Predominantly exploitation with small, informed perturbations.
- Strategy is now fully **per-function**, driven by empirical evidence rather than a single global heuristic.

Overall, this week demonstrates a mature optimisation mindset focused on **trust-region refinement, cautious rollback, and stability over aggressive exploration**.

---
