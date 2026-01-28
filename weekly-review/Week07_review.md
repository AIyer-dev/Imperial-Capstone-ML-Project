# Week 7 Review – Local Refinement, Diminishing Returns, and Plateau Testing

This document captures the **Week 7 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By this point, the optimisation has clearly entered a **late-stage refinement phase**, where most functions are either converging toward known optima or approaching plateaus.

---

## 1. Interpreting the Week 6 Results

Week 6 outputs provided several important signals that directly shaped the Week 7 strategy:

- **F4:** Large improvement and a new best value — strong evidence that the correct basin has been found.
- **F5:** Continued monotonic improvement — exploitation remains justified.
- **F6:** Rapid improvement toward zero — trend is strong but overshoot risk is increasing.
- **F7:** Close to the historical best — suggests fine local refinement rather than reset.
- **F8:** At or near the ceiling — likely plateau behaviour.
- **F2:** Performance worsened after a small nudge — ridge is narrow and sensitive.
- **F1:** Remains flat — useful only for controlled exploration.

Overall, Week 6 confirmed that most functions no longer require global exploration. Instead, **precision and restraint** are now the dominant concerns.

---

## 2. Strategic Focus for Week 7

The Week 7 strategy emphasised:

- **Local refinement** where new bests or strong trends appeared (F4, F5, F6).
- **Smaller step sizes** in sensitive regions (F2, F7).
- **Plateau testing** via tiny asymmetric perturbations (F8).
- **Purposeful exploration** only where structure remains absent (F1).

This reflects a classic late-stage BO posture: *confirm, refine, and avoid unnecessary risk.*

---

## 3. Week 7 Query Decisions (with Rationale)

### **F1 (2D – Flat Landscape)**
**Submitted:** `0.750000-0.250000`

Previous samples covered the centre and multiple corners/diagonals with near-zero outputs.  
Week 7 probes the **opposite diagonal** from Week 6, completing a controlled sweep of mid-space directions to confirm the absence of structure.

---

### **F2 (2D – Narrow Ridge Near x₂ ≈ 1)**
**Submitted:** `0.693750-0.999999`

A small performance drop in Week 6 indicated that the ridge is narrow and sensitive.  
Week 7 uses an **even smaller half-step** back toward the historically best region, refining cautiously rather than jumping.

---

### **F3 (3D – Persistent Week 1 Basin)**
**Submitted:** `0.950000-0.607000-0.865000`

The best result remains near the Week 1 configuration.  
Instead of fully resetting, Week 7 stays within the same basin and applies a **micro-perturbation** to test whether the optimum is slightly skewed.

---

### **F4 (4D – New Best in Week 6)**
**Submitted:** `0.420000-0.392000-0.348000-0.418000`

Week 6 delivered a significant improvement, strongly signalling the correct basin.  
Week 7 performs **tight trust-region refinement**, applying very small directional shifts to locate the precise peak.

---

### **F5 (4D – Monotonic Improvement Continues)**
**Submitted:** `0.250000-0.900000-0.999999-0.999999`

The improvement trend remains consistent: increasing *x₁* and *x₂* while keeping dimensions 3–4 saturated.  
Week 7 continues controlled exploitation with a modest step, preserving stability while climbing the peak.

---

### **F6 (5D – Rapid Convergence Toward Zero)**
**Submitted:** `0.410000-0.350000-0.570000-0.845000-0.125000`

Week 6 produced a large improvement, indicating strong gradient alignment.  
Week 7 maintains the same direction but **reduces step size**, guarding against overshoot as the optimum is approached.

---

### **F7 (6D – Near Historical Best)**
**Submitted:** `0.000000-0.442000-0.236000-0.148000-0.387000-0.675000`

Week 6 came close to the historical best from Week 2.  
Week 7 refines locally around this region, nudging the most influential dimensions (2, 4, and 6) to test whether the peak can be surpassed.

---

### **F8 (8D – Plateau / Ceiling Behaviour)**
**Submitted:**  
`0.805000-0.795000-0.805000-0.795000-0.999999-0.999999-0.999999-0.999999`

Repeated evaluations at the symmetric 0.8 configuration suggest plateau behaviour.  
Week 7 applies a **tiny asymmetric perturbation** to test whether the optimum is perfectly symmetric or slightly offset along certain dimensions.

---

## Summary

Week 7 represents a critical late-stage phase:

- Most functions are now in **local refinement or plateau testing**.
- Step sizes are deliberately small to minimise risk.
- Exploration is limited, targeted, and justified.
- Decisions prioritise **precision over novelty**.

This week further consolidates convergence and prepares the groundwork for the final confirmation and lock-in rounds.

---
