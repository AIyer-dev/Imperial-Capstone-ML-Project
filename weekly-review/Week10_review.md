# Week 10 Review – Lock-In, Micro-Refinement, and Late-Stage Control

This document captures the **Week 10 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By Week 10, the optimisation process has clearly entered a **lock-in and confirmation phase**, where most functions are either solved, plateaued, or require only extremely fine-grained refinement.

---

## 1. Strategic Context Going into Week 10

Results from Week 9 made the overall landscape very clear:

- **F1** shows no signal anywhere and can be treated as solved / irrelevant.
- **F5** continues to deliver the strongest and most reliable gains.
- **F8** is fully plateaued at a stable global maximum.
- **F2, F3, and F4** sit in narrow, sensitive basins requiring micro-adjustments only.
- **F6** has demonstrated instability after overshoot and now demands cautious rollback.
- **F7** is very close to its historical best and may still yield marginal gains.

Week 10 therefore focuses on **locking in known optima**, **correcting overshoot**, and **extracting any remaining marginal improvements** without destabilising performance.

---

## 2. Function-by-Function Week 10 Decisions

### **F1 (2D – Fully Flat, No Signal)**
**Submitted:** `0.500000-0.500000`

Week 9 again produced a near-zero output, consistent with the entire history of this function.  
There is no justification for further exploration. From Week 10 onward, this function is effectively **frozen**, conserving budget and attention.

---

### **F2 (2D – Narrow Ridge, Below Historical Best)**
**Submitted:** `0.693000-0.999999`

Week 9 recovered relative to Week 8 but remains below the Week 4 peak (≈0.699).  
The ridge along *x₂ ≈ 1* remains narrow and noisy. Week 10 applies a **very fine corrective step upward in *x₁***, staying strictly within the known good band to avoid oscillation.

---

### **F3 (3D – Basin with Gradual Recovery)**
**Submitted:** `0.947000-0.612000-0.872000`

Week 9 showed further improvement (≈ −0.029), confirming continued descent within the basin.  
Week 10 continues local refinement, slightly increasing *x₂* and *x₃* while keeping *x₁* near the basin centre to probe curvature without resetting.

---

### **F4 (4D – Near a Local Optimum)**
**Submitted:** `0.417000-0.387000-0.351000-0.413000`

Week 9 recovered performance close to the Week 6 maximum but did not exceed it.  
This strongly suggests the optimum lies in a **very narrow region**. Week 10 tightens the trust region further, making only **micro-adjustments** to refine the local maximum.

---

### **F5 (4D – Chemical Yield, Strong Monotonic Growth)**
**Submitted:** `0.280000-0.960000-0.999999-0.999999`

Week 9 produced another substantial gain (≈3732), with no evidence of saturation.  
This remains the highest-return function. Week 10 continues exploitation with a **controlled but meaningful step** in *x₁* and *x₂*, while keeping dimensions 3 and 4 fixed at their empirically optimal values.

---

### **F6 (5D – Overshoot and Stability Reset)**
**Submitted:** `0.400000-0.340000-0.560000-0.860000-0.110000`

Week 9 worsened further (≈ −0.272), confirming instability after recent steps.  
Week 10 deliberately **rolls back toward the Week 7 region**, prioritising stability and basin re-entry over forward progress. This is a reset *within* the trust region, not a restart.

---

### **F7 (6D – Near Historical Best, Late-Stage Refinement)**
**Submitted:** `0.000000-0.446000-0.233000-0.150000-0.388000-0.670000`

Week 9 improved to ≈1.421, approaching the Week 2 best (≈1.433).  
This suggests the optimum is nearby. Week 10 applies **very small asymmetric nudges** to test whether the historical peak can be surpassed without destabilising performance.

---

### **F8 (8D – Hard Plateau Confirmed)**
**Submitted:**  
`0.800000-0.800000-0.800000-0.800000-0.999999-0.999999-0.999999-0.999999`

Week 9 again returned the global best value, confirming a stable and symmetric plateau.  
Week 10 keeps this configuration fixed, effectively **locking in performance** while optimisation effort is focused elsewhere.

---

## 3. Strategic View – Where You Are Now

By Week 10, the optimisation posture is clear:

- **Actively pushing:** F5
- **Micro-refining:** F2, F3, F4, F7
- **Stabilising / correcting:** F6
- **Locked-in / frozen:** F1, F8

This is exactly the posture expected at this stage of a Bayesian Optimisation process:  
**discipline over novelty**, careful control over step sizes, and explicit recognition of plateaus and instability.

Week 10 marks the transition from optimisation to **final validation and confirmation** in the remaining rounds.

---
