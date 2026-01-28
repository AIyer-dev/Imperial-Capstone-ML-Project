# Week 5 Review – Confirmation, Rollback, and Peak Refinement

This document captures the **Week 5 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
Week 5 represents a transition into a **confirmation-driven phase**, where most decisions are informed by comparing recent outcomes against earlier basins and correcting oversteps.

---

## 1. Quick Review of Week 4 Results

Comparing Week 4 outputs to earlier weeks revealed clear patterns:

- **F1:** Outputs remain essentially zero across all weeks → function appears flat.
- **F2:** Week 4 achieved a new best (≈0.6992), slightly improving on Week 1.
- **F3:** Week 4 improved relative to Week 3, but Week 1 remains the best.
- **F4:** Sharp regression in Week 4 (0.118) after a strong Week 3 (0.518) → evidence of stepping out of a narrow basin.
- **F5:** Monotonic improvement overall; Week 4 produced the best yield so far (≈2941).
- **F6:** Steady improvement each week; Week 4 is the least negative (best so far).
- **F7:** Best result still from Week 2; Week 4 recovered from Week 3 but did not surpass it.
- **F8:** Best remains Week 2; Weeks 3–4 stayed in the same high region but slightly worse.

Overall, these results confirmed that **local refinements dominate performance**, and large deviations risk regression.

---

## 2. Function-by-Function Week 5 Strategy

### **F1 (2D – Flat Landscape)**
**Submitted:** `0.500000-0.500000`

Four distinct corners of the space have already been tested with near-zero outputs. With no evidence of structure, exploitation is meaningless.  
Week 5 therefore probed the **centre of the domain**, testing whether any hidden structure exists away from boundaries.

---

### **F2 (2D – Ridge Near x₂ ≈ 1)**
**Submitted:** `0.695000-0.999999`

Evidence now strongly supports a ridge near *x₂ ≈ 1* and *x₁ ≈ 0.69–0.70*.  
Week 5 performed a **very fine exploitation step**, nudging *x₁* from 0.69 to 0.695 while keeping *x₂* fixed at its best-known value. This is classic peak refinement along a ridge.

---

### **F3 (3D – Basin Near Week 1 Region)**
**Submitted:** `0.930000-0.620000-0.880000`

The best output remains from Week 1, but Weeks 3–4 have approached that region without surpassing it.  
Week 5 exploited around the **Week 1 basin**, making a small directional adjustment to test whether the optimum lies slightly offset from the original point.

---

### **F4 (4D – Narrow Basin, Rollback Required)**
**Submitted:** `0.420000-0.380000-0.360000-0.400000`

Week 4’s sharp drop after a strong Week 3 result indicated an overshoot.  
Week 5 explicitly **stepped back toward the Week 3 configuration**, but in the opposite direction of the Week 4 move. This probes the other side of the narrow basin while remaining close to the known peak.

---

### **F5 (4D – Chemical Yield, Unimodal Peak)**
**Submitted:** `0.230000-0.870000-0.999999-0.999999`

F5 continues to behave like a smooth unimodal surface. Ignoring the early dip, increases in *x₁* and *x₂* have consistently raised yield, while dimensions 3 and 4 clearly prefer the upper boundary.  
Week 5 continued **pure exploitation**, taking another careful step upward in *x₁* and *x₂* while holding the critical dimensions fixed.

---

### **F6 (5D – Gradual Improvement Gradient)**
**Submitted:** `0.380000-0.320000-0.500000-0.860000-0.090000`

Outputs have improved monotonically from Week 1 to Week 4 as the search followed a consistent gradient direction.  
Week 5 continued along this same direction with **modest step sizes**, balancing exploitation with micro-exploration to avoid overshooting.

---

### **F7 (6D – Hyperparameter Basin, Return to Best)**
**Submitted:** `0.000000-0.450000-0.233000-0.155000-0.386000-0.670000`

Week 2 remains the global best for F7. Weeks 3–4 moved away and performed worse.  
Week 5 therefore returned close to the Week 2 configuration, making only tiny adjustments. This is equivalent to **zooming in on a known good hyperparameter basin** rather than continuing speculative exploration.

---

### **F8 (8D – High-Dimensional Basin Near 0.8)**
**Submitted:**  
`0.800000-0.820000-0.800000-0.780000-0.999999-0.999999-0.999999-0.999999`

Week 2 remains the best configuration. Subsequent weeks stayed nearby but did not improve.  
Week 5 refined within the same basin by applying **small asymmetric perturbations** around 0.8 in the first four dimensions while keeping the remaining dimensions fixed at their empirically optimal values.

---

## Summary

Week 5 solidified the optimisation strategy:

- **F1:** Continued exploration due to complete lack of structure.
- **F2–F8:** Predominantly exploitation with trust-region refinement.
- Explicit **rollback and correction** (F4, F7) after detecting regressions.
- Strong emphasis on **confirmation and stability** rather than aggressive improvement.

This week marks the point where optimisation decisions are driven primarily by **evidence consolidation**, setting the stage for later confirmation and lock-in rounds.

---
