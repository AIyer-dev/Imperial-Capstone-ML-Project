# Week 1 Review – Black-Box Optimisation Results

This document summarises the **Week 1 / early-stage review** of optimisation performance across all eight black-box functions.  
The focus at this stage was **diagnosis rather than optimisation**, identifying early signals about function structure, noise, and promising regions.

---

## Summary Table

| Function | Output (Week 2) | Change / Observation | Interpretation |
|---------|------------------|----------------------|----------------|
| **F1** | −4.66 × 10⁻⁵⁹ | No measurable improvement (still near 0) | Function likely has an extremely flat region or a hidden narrow optimum elsewhere. Model uncertainty is likely very high. |
| **F2** | 0.691784 | Moderate output; likely improvement from previous low values | Encouraging. Region near *(0.7, 1.0)* may be close to a local optimum — suitable for fine exploitation. |
| **F3** | −0.044084 | Slightly negative; comparable to earlier results | Still weak performance; function may be noisy or non-smooth. Broader exploration is required. |
| **F4** | 0.455522 | Moderate positive output | GP prediction aligned well. Possible ridge-like structure — continue local exploitation. |
| **F5** | 2523.61 | Strong improvement; clear high-performing region identified | Unimodal assumption appears valid. Subsequent rounds should exploit this neighbourhood to refine performance. |
| **F6** | −1.1573 | Worse performance (still negative) | Model likely misled by local minima; exploratory sampling is needed. |
| **F7** | 1.08066 | Improved relative to earlier results | Hybrid exploration–exploitation strategy performing well; continue moderate exploration. |
| **F8** | 3.09832 | Strong output | Likely operating in a high-performing region; stability should be verified using diverse samples. |

---

## Key Observations

- **Exploration was essential at this stage**: Several functions (notably F1, F3, and F6) showed little exploitable structure, reinforcing the need for broad sampling rather than early exploitation.
- **Early signals of structure emerged** for F2, F4, F5, and F7, suggesting ridges or unimodal behaviour that could be exploited in later rounds.
- **F5 stood out clearly** as the most promising function early on, justifying increased focus in subsequent iterations.
- **Model uncertainty remained high** across most functions, making this phase primarily diagnostic rather than optimisation-driven.

---

## Strategic Takeaway (Week 1)

Week 1 served as a **landscape-mapping phase**. The primary success criterion was not maximising outputs, but identifying which functions:
- were flat or uninformative,
- required further exploration,
- or showed early promise for structured optimisation.

These insights directly informed the transition into more targeted strategies in later weeks.

---
