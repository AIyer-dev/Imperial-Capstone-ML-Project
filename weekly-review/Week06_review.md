# Week 6 Review – Consolidation, Confidence, and High-Value Refinement

This document captures the **Week 6 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
Week 6 represents a clear **mid-to-late optimisation phase**, where the emphasis shifts toward **high-confidence exploitation**, supported by stabilised empirical evidence from earlier rounds.

---

## 1. Review of Week 5 Results – What Actually Happened

Analysis of the Week 5 outputs revealed several important stabilising patterns:

### Objective-Level Behaviour
- Large positive objective values are now consistently observed, particularly for **F5**, which operates in the ~2500–3100 range.
- This strongly indicates that the optimisation has located **genuine high-value basins**, rather than sampling noise.
- Functions that previously produced near-zero or extreme negative values have stabilised, suggesting early exploratory uncertainty has diminished.

### Function-Wise Observations
- **F5:** Clear monotonic improvement across iterations — a strong exploitation signal.
- **F8:** Outputs are consistently high and stable (~5.0–5.26), indicating near-plateau behaviour.
- **Lower-scale functions (F1–F4):** Still noisy, but significantly less erratic than in early weeks.

Collectively, these results mark a transition from **global exploration** into **local refinement of promising regions**.

---

## 2. What the Week 5 Inputs Reveal About Strategy

The Week 5 input patterns show a noticeably more mature query strategy:

### Reduced Randomness
- Inputs are no longer scattered uniformly across the domain.
- Many dimensions now cluster within mid-to-high ranges (≈0.65–0.95), reflecting informed narrowing of the search space.

### Soft Exploitation
- For functions such as **F5–F8**, queries implicitly focus on known high-performing regions.
- Importantly, the strategy has not fully collapsed to identical points, preserving some exploratory flexibility.

### Constraint Awareness
- Repeated use of boundary values (e.g. `0.999999`) shows awareness of saturation effects and hard limits in the black-box functions.

Overall, this reflects a **late-capstone optimisation posture**: deliberate, informed, and balanced rather than greedy or naïve.

---

## 3. Strategic Reflection (Assessment-Relevant)

By Week 5, the evolution of strategy is clear:

- **Early weeks:** Broad exploration, weak signal, high variance.
- **Middle weeks:** Pattern recognition and basin identification.
- **Week 5 onward:** Focused exploitation with controlled exploration.

This progression aligns closely with **Bayesian Optimisation best practice** and demonstrates exactly the kind of adaptive reasoning expected in this capstone.

---

## 4. What Week 6 Should Achieve (Key Decision Point)

Week 6 should **not** reset the search. Instead, it should consolidate gains:

### Double Down On
- Local refinement for high-performing functions (**especially F5 and F8**).
- Small perturbations around best-known configurations.

### Avoid
- Large random jumps (wastes limited remaining budget).
- Repeated identical submissions that risk stagnation.

### Target Behaviour
- **80–85% exploitation**
- **15–20% structured exploration** (small-radius, not global)

---

## 5. Week 6 Query Decisions (with Rationale)

### **F1 (2D – Effectively Flat)**
**Submitted:** `0.250000-0.750000`

Outputs remain near zero regardless of location. With one query available, exploitation is unjustified.  
Week 6 probes a **new mid-space diagonal**, neither corner nor centre, in case hidden structure exists elsewhere.

---

### **F2 (2D – Ridge Near x₂ ≈ 1)**
**Submitted:** `0.692500-0.999999`

The best value occurred near *x₁ ≈ 0.69*.  
Week 6 makes a **tiny trust-region refinement**, nudging slightly upward along the ridge to test if the peak lies just above the previous optimum.

---

### **F3 (3D – Best Basin from Week 1)**
**Submitted:** `0.955000-0.600000-0.870000`

The strongest result remains from Week 1, with later samples approaching but not surpassing it.  
Week 6 stays within the same basin, applying a small directional nudge to test for a nearby skewed optimum.

---

### **F4 (4D – Narrow Basin, New Best in Week 5)**
**Submitted:** `0.415000-0.385000-0.355000-0.410000`

Week 5 produced the best value so far, supported by nearby strong results in Week 3.  
Week 6 refines this basin with a **small asymmetric perturbation**, balancing exploitation with caution.

---

### **F5 (4D – Chemical Yield, Strong Monotonic Signal)**
**Submitted:** `0.240000-0.880000-0.999999-0.999999`

Yield has increased as *x₁* and *x₂* rose, while dimensions 3 and 4 remained saturated.  
Week 6 continues along the same gradient direction with a **small step**, avoiding overshoot while exploiting a clear peak.

---

### **F6 (5D – Recipe Score, Gradual Improvement)**
**Submitted:** `0.400000-0.340000-0.550000-0.850000-0.110000`

Outputs have steadily improved (become less negative) following a consistent direction of movement.  
Week 6 continues this trust-region exploitation with a **modest but meaningful step**.

---

### **F7 (6D – Hyperparameters, Return to Known Best)**
**Submitted:** `0.000000-0.440000-0.235000-0.150000-0.385000-0.665000`

Week 2 remains the best-performing configuration.  
Week 6 zooms back toward this basin with very small adjustments, checking whether the true optimum lies just off the Week 2 point.

---

### **F8 (8D – High-Dimensional Plateau)**
**Submitted:**  
`0.800000-0.800000-0.800000-0.800000-0.999999-0.999999-0.999999-0.999999`

The symmetric configuration from Week 2 remains the best.  
With one query available, Week 6 prioritises **highest-confidence exploitation**, re-submitting the known peak rather than spending budget on exploration.

---

## Summary

Week 6 reflects a confident, evidence-driven optimisation stage:

- Clear shift toward **consolidation and confirmation**.
- High-performing functions are exploited with care and precision.
- Exploration is limited, structured, and justified.
- Decisions prioritise **stability and empirical confidence** over speculative gains.

This week sets up a strong foundation for the final convergence and lock-in phases of the capstone.

---
