# Week 8 Review – Stabilisation, Fine-Grained Refinement, and Plateau Confirmation

This document captures the **Week 8 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By Week 8, the optimisation process is firmly in a **late-stage regime**, characterised by stabilisation of high-performing functions, fine-grained refinement of sensitive ridges, and confirmation of plateaus.

---

## 1. Strategic Context Going into Week 8

Results from Week 7 indicated that:

- Several functions are **near convergence** (F4, F6, F7).
- Others are exhibiting **clear plateau behaviour** (F1, F8).
- A subset continues to show **strong monotonic growth** (F5).
- Narrow, noisy structures require **extremely cautious refinement** (F2, F3).

As a result, Week 8 prioritised **stability and precision** over aggressive optimisation, with step sizes shrinking further across most functions.

---

## 2. Function-by-Function Week 8 Decisions

### **F1 (2D – Consistently Flat)**
**Submitted:** `0.500000-0.500000`

Week 7 again produced an effectively zero output, consistent with all previous iterations.  
There is no empirical evidence of structure anywhere in the domain. Re-submitting the centre in Week 8 is a **neutral, low-risk decision**, effectively deprioritising optimisation effort on this function.

---

### **F2 (2D – Narrow Ridge Near x₂ ≈ 1)**
**Submitted:** `0.694500-0.999999`

Week 7 recovered performance after a dip in Week 6, confirming the ridge structure near *x₂ ≈ 1*.  
However, sensitivity along *x₁* remains high. Week 8 applies a **very small interpolation step** between the best historical values (≈0.693–0.695), refining the ridge without inducing oscillation.

---

### **F3 (3D – Gradual Basin Approach)**
**Submitted:** `0.948000-0.608000-0.868000`

Week 7 improved noticeably compared to Week 6, indicating continued movement toward the basin floor, even though the absolute best remains from Week 1.  
Week 8 continues **local refinement in the same direction**, as gradient signal is still present and a full reset would discard useful information.

---

### **F4 (4D – Refining Between Competing Peaks)**
**Submitted:** `0.418000-0.388000-0.350000-0.415000`

A slight drop in Week 7 after the Week 6 peak suggests the optimum lies between those two configurations.  
Week 8 positions itself **midway between Weeks 6 and 7**, tightening the trust region to recapture the local maximum while avoiding overshoot.

---

### **F5 (4D – Chemical Yield, Strong Monotonic Growth)**
**Submitted:** `0.260000-0.920000-0.999999-0.999999`

Week 7 produced another substantial increase (≈3340), reinforcing the monotonic trend.  
No signs of saturation are visible. Week 8 continues exploitation with a slightly larger step in *x₁* and *x₂*, while keeping dimensions 3 and 4 fixed at their empirically optimal boundary.

---

### **F6 (5D – Approaching Convergence)**
**Submitted:** `0.420000-0.360000-0.580000-0.840000-0.135000`

Week 7 improved again, but the magnitude of gains has slowed, indicating proximity to the optimum.  
Week 8 maintains the same search direction with a **smaller step size**, consistent with late-stage trust-region optimisation.

---

### **F7 (6D – Sensitive Basin, Partial Regression)**
**Submitted:** `0.000000-0.445000-0.234000-0.150000-0.386000-0.670000`

Week 7 regressed slightly after nearing the peak in Week 6, suggesting a sensitive rather than flat optimum.  
Week 8 moves back toward the historically strongest configuration, but stops short of snapping fully to the Week 2 best, preserving learning capacity for remaining weeks.

---

### **F8 (8D – Plateau with Minor Noise)**
**Submitted:**  
`0.800000-0.800000-0.800000-0.800000-0.999999-0.999999-0.999999-0.999999`

Asymmetric perturbations in Week 7 produced slightly worse results, reinforcing that the symmetric configuration remains optimal.  
Week 8 therefore **locks back onto the plateau centre**, prioritising stability and confirmation over further exploration.

---

## Summary

Week 8 is characterised by:

- **Stabilisation of converged functions** (F1, F8).
- **Extremely fine-grained refinement** of sensitive ridges and basins (F2–F4, F6–F7).
- Continued **strong exploitation** where monotonic growth persists (F5).
- A deliberate reduction in step sizes across most functions.

This week represents a mature late-capstone phase focused on **precision, confirmation, and risk minimisation**, laying the groundwork for final lock-in and validation rounds.

---
