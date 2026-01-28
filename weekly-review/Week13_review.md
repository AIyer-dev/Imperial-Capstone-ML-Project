# Week 13 Review – Final Outcomes and What They Reveal

This document captures the **final Week 13 reflection** for the Black-Box Optimisation (BBO) capstone, focusing not on whether every function improved in the last round, but on **what the final outcomes reveal about the underlying landscapes**.

At this stage, success is measured by *correct interpretation*, not by marginal gains.

---

## 🔍 What Happened in the Final Round (Week 13)?

### **F1 – Flat Function**
- **Final output:** ~0  
- **What happened:** Nothing changed — and that is exactly what should have happened.  
- **Interpretation:**  
  F1 is effectively constant across the entire domain. Early exploration correctly identified the absence of structure, and freezing the function at a neutral point was optimal.  
  **✅ Correct early diagnosis, correct final behaviour.**

---

### **F2 – Narrow Ridge**
- **Final output:** ~0.747  
- **What happened:**  
  The final submission landed back near the ridge, recovering strong performance after mid-project oscillations.  
- **Interpretation:**  
  This confirms that F2 has a sharp ridge near *x₂ ≈ 1*, with high sensitivity in *x₁*. The volatility observed mid-project was not noise, but true ridge sensitivity.  
  **✅ Late-stage rollback and lock-in worked exactly as intended.**

---

### **F3 – Local Basin**
- **Final output:** ~−0.033  
- **What happened:**  
  Slightly worse than the best historical value (~−0.027), but clearly within the same basin.  
- **Interpretation:**  
  F3 has a broad, shallow basin. Differences at this scale are likely numerical rather than strategic.  
  **🟡 Effectively converged; minor fluctuation is expected.**

---

### **F4 – Plateau with Traps**
- **Final output:** ~0.456  
- **What happened:**  
  The final result fell below the global best (~0.605).  
- **Interpretation:**  
  F4 contains multiple local plateaus. The final point landed on a secondary plateau rather than the global one. Importantly, the true global best *was* discovered earlier.  
  **🟡 Not a failure — this reveals genuine landscape complexity.**

---

### **F5 – Strong Monotonic Growth (with Saturation)**
- **Final output:** ~2524  
- **What happened:**  
  The final value dropped sharply relative to the peak (~4459).  
- **Interpretation:**  
  This is a classic overshoot/saturation effect. The function rewards increasing *x₁* and *x₂* up to a threshold, after which performance collapses.  
  Crucially, the true optimum was already identified earlier.  
  **🟡 Confirms nonlinearity, not strategy failure.**

---

### **F6 – Highly Unstable / High-Variance**
- **Final output:** ~−1.16  
- **What happened:**  
  Performance regressed sharply in the final round.  
- **Interpretation:**  
  F6 is extremely sensitive, with small perturbations producing large swings. The final regression validates earlier conclusions about instability rather than contradicting them.  
  **🟡 High variance, not poor reasoning.**

---

### **F7 – Clear Global Optimum**
- **Final output:** ~1.433  
- **What happened:**  
  The final round exactly matched the global best first observed in Week 2.  
- **Interpretation:**  
  This is a textbook case of early discovery of a strong global optimum, followed by correct long-term convergence and confirmation.  
  **✅ Perfect convergence behaviour.**

---

### **F8 – Hard Plateau**
- **Final output:** ~5.2623  
- **What happened:**  
  Identical to many previous rounds.  
- **Interpretation:**  
  F8 exhibits a flat saturation plateau. Once reached, further optimisation yields no change. Freezing this configuration was optimal.  
  **✅ Exactly what a saturated function should do.**

---

## 🧠 Big-Picture Interpretation (Key Takeaway)

The final results should not be interpreted as “did every function improve in Week 13?”, but rather:

- You correctly identified **distinct landscape types**:
  - flat (F1),
  - ridge (F2),
  - basin (F3),
  - multi-plateau (F4),
  - monotonic but nonlinear (F5),
  - unstable / high-variance (F6),
  - clean global optimum (F7),
  - hard saturation (F8).
- You **adapted strategy appropriately** for each landscape.
- Where the final round underperformed, it **revealed structure**, not error.
- In several cases (F1, F7, F8), the final result *perfectly confirms* long-term reasoning.

This is exactly how a **professional optimisation story should end**:

> The final iteration validates the learned structure of the problem,  
> even when it does not improve performance.

That validation — not last-step improvement — is the true success of the optimisation process.

---
