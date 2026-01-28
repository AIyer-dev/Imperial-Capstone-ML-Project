# Week 11 Review – Optimisation Through a Clustering Lens

This document captures the **Week 11 strategy reflection** for the Black-Box Optimisation (BBO) capstone.  
By the eleventh iteration, the optimisation process is best understood through a **clustering perspective**, where the search space is no longer treated as continuous and uniform, but instead as a collection of emergent regions with distinct behavioural patterns.

Rather than searching for isolated optima, the focus has shifted toward **identifying, stabilising, and refining clusters of high-performing points**, while tightening boundaries around regions that consistently underperform.

---

## 1. How Have Patterns in Past Queries Influenced Week 11 Choices?

Patterns observed across the first ten rounds played a central role in shaping the Week 11 strategy.

Several functions repeatedly produced strong performance within narrow neighbourhoods, while others showed either flat responses or instability when moved too far from known good regions. These observations motivated a shift toward **centroid refinement**: selecting points near the centre of historically strong regions rather than probing new territory.

Where previous perturbations caused sharp drops in performance, Week 11 deliberately **rolled back toward the densest region of successful samples** instead of continuing outward exploration. This reflects an explicit preference for stability and consolidation over novelty.

---

## 2. Identification of Clusters in the Search Space

Clear clusters emerged for multiple functions:

- **Tight basin clusters:**  
  Some functions exhibit compact regions where small deviations remain performant, indicating well-defined local optima with strong local smoothness.

- **Directional corridor clusters:**  
  Other functions, particularly those with monotonic trends, form elongated clusters aligned with a dominant direction of improvement rather than a single peak.

- **Non-clustering functions:**  
  A subset of functions show no meaningful clustering at all, with outputs remaining flat regardless of input. These functions were effectively deprioritised, as further optimisation effort is unlikely to yield gains.

Recognising these different cluster types allowed for **function-specific refinement strategies**, rather than forcing a one-size-fits-all optimisation approach.

---

## 3. Which Strategies Proved Less Effective, and How Were They Adjusted?

Late-stage strategies that attempted broader exploration proved consistently ineffective, often yielding worse outcomes than conservative refinements around known strong regions.

Additionally, **symmetric probing** around optima occasionally underperformed, suggesting that some clusters are slightly skewed rather than perfectly centred. In response, Week 11 adjustments prioritised:

- **Asymmetric, small-radius movements** around cluster centroids.
- **Rollback to historically strong configurations** when instability was detected.
- Avoidance of exploratory jumps that disrupt established clusters.

This reflects a clear shift away from novelty-seeking behaviour and toward consolidation and robustness.

---

## 4. Parallels with Clustering Algorithms: Separating Signal from Noise

The Week 11 refinement process closely mirrors how clustering algorithms separate signal from noise:

- Early iterations resemble **density discovery**, identifying where points begin to concentrate.
- As more data accumulates, **low-density regions are implicitly discarded**, while high-density regions attract further refinement.
- Boundary tightening in Week 11 parallels how clustering algorithms refine cluster borders once centroids are established.
- Erratic performance far from cluster centres is treated as noise and increasingly ignored.

This analogy provides a useful mental model for understanding why late-stage optimisation focuses on stabilisation rather than exploration.

---

## 5. Expected Visual Patterns if Results Were Plotted

If query results were visualised:

- Some functions would show **tight, well-separated clusters** of high-performing points with steep drop-offs outside the cluster.
- Others would show **elongated clusters** aligned with a dominant axis, reflecting monotonic improvement rather than a single peak.
- Flat functions would appear as near-uniform scatter with no visible grouping.

These visual patterns directly inform decision-making, indicating whether further refinement should occur within an existing cluster, whether boundaries should be tightened further, or whether convergence has effectively been reached.

---

## Overall Reflection

By Week 11, the optimisation process has transitioned from searching the space to **managing clusters within it**.  
The strategy now prioritises:

- Distance-aware refinement,
- Centroid stability,
- Boundary tightening,
- And robustness over aggressive improvement.

This cluster-oriented perspective reduces sensitivity to noise, improves interpretability, and aligns closely with how unsupervised learning methods identify and refine meaningful structure in high-dimensional data. It also positions the remaining iterations to focus on **confirmation and final consolidation**, rather than rediscovery.

---
