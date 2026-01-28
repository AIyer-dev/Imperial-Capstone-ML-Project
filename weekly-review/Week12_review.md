# Week 12 Review – Centroid Confirmation and Final Consolidation

This document captures the **Week 12 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
At this stage, the optimisation process has fully transitioned into **confirmation and consolidation**, where the primary goal is to validate previously identified optima and stabilise performance rather than discover new regions.

Week 12 is deliberately conservative and reflects professional late-stage optimisation practice.

---

## 1. High-Level Assessment After Week 11

By the end of Week 11, the behaviour of each function was well characterised:

- **F5:** Continues to improve strongly → one final controlled push is justified.
- **F2:** Clear recovery back onto the ridge → centroid confirmation is appropriate.
- **F3:** Stabilised near the best local basin → confirmation, not exploration.
- **F4:** Plateau confirmed → lock the best region.
- **F6:** Best value so far achieved → confirm and do *not* move.
- **F7:** Improved again but still slightly below global best → tiny centroid tightening.
- **F1, F8:** Fully converged or flat → freeze.

Given this landscape, Week 12 focuses on **centroid confirmation**, boundary tightening, and risk minimisation.

---

## 2. Week 12 Query Decisions (with Rationale)

### **F1 (2D – Flat, Fully Converged)**
**Submitted:** `0.500000-0.500000`

No signal has been observed across all weeks. Re-submitting a neutral centre reinforces convergence and avoids introducing unnecessary variance.

---

### **F2 (2D – Ridge, Centroid Confirmation)**
**Submitted:** `0.692000-0.999999`

Week 11 recovered strongly (≈0.692), confirming the ridge centroid near *x₁ ≈ 0.69* and *x₂ ≈ 1*.  
Week 12 confirms this cluster centre rather than stepping again, prioritising stability over marginal exploration.

---

### **F3 (3D – Basin, Confirm Best Local Cluster)**
**Submitted:** `0.948000-0.608000-0.868000`

This configuration corresponds to the best-performing local basin observed so far.  
Week 12 re-samples the **cluster centroid** to confirm stability rather than perturbing a sensitive basin.

---

### **F4 (4D – Plateau, Lock Best Region)**
**Submitted:** `0.416000-0.386000-0.352000-0.412000`

Performance has plateaued around ~0.60–0.61.  
This point sits at the centre of the tight cluster formed between Weeks 6 and 11. Week 12 confirms that the plateau is stable.

---

### **F5 (4D – Chemical Yield, Final Controlled Exploitation)**
**Submitted:** `0.300000-0.999000-0.999999-0.999999`

Week 11 reached a new high (≈4203), and the monotonic trend still holds.  
However, saturation is approaching. Week 12 makes a **very small final step** in *x₁* and *x₂* before full lock-in in Week 13.

---

### **F6 (5D – Recipe, Best Value Achieved)**
**Submitted:** `0.400000-0.340000-0.560000-0.860000-0.110000`

Week 11 produced the best value so far (≈ −0.160).  
Given prior instability, Week 12 deliberately **confirms rather than moves**. Any change risks overshoot and regression.

---

### **F7 (6D – Hyperparameters, Tighten Around Improving Cluster)**
**Submitted:** `0.000000-0.445000-0.233000-0.150000-0.387000-0.670000`

Week 11 improved again (≈1.429), close to the global best (≈1.433).  
This tiny centroid tightening tests whether the cluster centre slightly outperforms both Week 11 and the historical peak.

---

### **F8 (8D – Plateau, Fully Converged)**
**Submitted:**  
`0.800000-0.800000-0.800000-0.800000-0.999999-0.999999-0.999999-0.999999`

Repeated maximum values across many weeks confirm a hard plateau.  
This configuration remains frozen through Week 12 (and into Week 13).

---

## 3. Strategic View – Where You Are Now

By Week 12, the optimisation posture is unequivocal:

- **Final push:** F5
- **Centroid confirmation:** F2, F3, F4, F6, F7
- **Frozen / converged:** F1, F8

This is exactly what a mature Bayesian Optimisation process looks like near termination:  
**confirmation over discovery, stability over novelty, and disciplined risk control.**

Week 12 positions the final iteration (Week 13) to serve as a clean **lock-in and validation round**, completing the optimisation narrative.

---
