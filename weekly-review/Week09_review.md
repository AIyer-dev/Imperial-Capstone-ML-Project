# Week 9 Review – Correction, Consolidation, and Late-Stage Discipline

This document captures the **Week 9 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By Week 9, the optimisation process is firmly in a **late-stage regime**, where the dominant themes are correction after overshoot, consolidation of strong basins, and disciplined avoidance of unnecessary exploration.

---

## 1. Strategic Context Going into Week 9

Results from Week 8 reinforced several important patterns:

- **F5** continues to show strong, monotonic improvement with no sign of saturation.
- **F8** has clearly reached a stable plateau at the symmetric configuration.
- **F1** remains flat with no detectable structure.
- **F2, F3, F4, and F6** exhibit sensitivity to small perturbations, indicating narrow basins and the risk of overshooting.
- **F7** remains stable but has not surpassed its historical peak.

As a result, Week 9 prioritised **correction and consolidation** rather than aggressive optimisation.

---

## 2. Function-by-Function Week 9 Decisions

### **F1 (2D – No Observable Signal)**
**Submitted:** `0.500000-0.500000`

Week 8 again produced a near-zero output, consistent with all prior iterations.  
There is no evidence of structure anywhere in the domain. Week 9 therefore maintains a **neutral centre point**, deprioritising optimisation effort while preserving consistency.

---

### **F2 (2D – Narrow, Noisy Ridge)**
**Submitted:** `0.692000-0.999999`

Week 8 dipped relative to the historical best (≈0.699 in Week 4), confirming that the ridge along *x₂ ≈ 1* is narrow and sensitive in *x₁*.  
Rather than oscillating, Week 9 applies a **very small corrective step** slightly below the historical best, keeping *x₂* saturated while refining cautiously along the ridge.

---

### **F3 (3D – Local Basin, High Sensitivity)**
**Submitted:** `0.946000-0.610000-0.870000`

Week 8 worsened slightly relative to Week 7, indicating sensitivity near the basin floor.  
However, performance remains substantially better than early weeks, suggesting proximity to a local optimum. Week 9 stays within the same basin, nudging *x₂* and *x₃* upward while slightly reducing *x₁* to probe curvature rather than resetting.

---

### **F4 (4D – Refinement Toward the Week 6 Peak)**
**Submitted:** `0.416000-0.386000-0.352000-0.412000`

Week 8 recovered some performance after the Week 7 dip but did not exceed the Week 6 maximum.  
This suggests the optimum lies between recent points. Week 9 further **tightens the trust region**, applying a midpoint-style adjustment to refine the local maximum.

---

### **F5 (4D – Chemical Yield, Strong Monotonic Growth)**
**Submitted:** `0.270000-0.940000-0.999999-0.999999`

Week 8 delivered another large improvement (≈3527), confirming a strong and consistent gradient.  
There is still no indication of saturation. Week 9 continues exploitation with a slightly larger step in *x₁* and *x₂*, while keeping dimensions 3 and 4 fixed at their clearly optimal values.

---

### **F6 (5D – Overshoot and Rollback)**
**Submitted:** `0.410000-0.350000-0.570000-0.850000-0.120000`

Week 8 regressed significantly (≈ −0.252), signalling overshoot in one or more dimensions.  
Week 9 deliberately **rolls back toward the Week 7 region**, reducing step size and re-establishing a stable trust region rather than pushing further.

---

### **F7 (6D – Stable but Below Peak)**
**Submitted:** `0.000000-0.444000-0.234000-0.152000-0.386000-0.668000`

Week 8 showed modest recovery but still did not surpass the Week 2 optimum.  
Week 9 remains close to the historically strong region, using **very small perturbations** to preserve accumulated knowledge while keeping learning potential alive.

---

### **F8 (8D – Plateau Confirmed)**
**Submitted:**  
`0.800000-0.800000-0.800000-0.800000-0.999999-0.999999-0.999999-0.999999`

Week 8 returned to the global best value, confirming a stable plateau.  
Week 9 re-submits the symmetric configuration to stabilise performance and minimise variance while remaining budget is conserved.

---

## 3. Strategic View – Where the Optimisation Stands

By Week 9, the overall posture is clear:

- **Still worth pushing:** F5 (clear monotonic gains).
- **Refine cautiously:** F2, F3, F4, F6.
- **Stabilise / hold:** F7, F8.
- **Effectively solved or flat:** F1.

This is exactly the posture expected in Weeks 9–10 of a well-executed BO process:  
**disciplined exploitation with controlled corrections**, avoiding both premature lock-in and wasteful exploration.

---
