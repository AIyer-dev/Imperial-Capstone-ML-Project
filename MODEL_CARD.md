# Model Card: BBO Optimisation Approach

## Overview
- Model name: Iterative Bayesian Black-Box Optimisation (BBO)
- Type: Sequential, query-based optimisation strategy
- Version: Capstone implementation (Weeks 1–13)
- Approach: Heuristic Bayesian optimisation with manual trust-region refinement

## Intended Use
This approach is suitable for optimisation problems with expensive or opaque objective functions and low evaluation budgets. It is not suitable for high-dimensional problems requiring global guarantees or fully automated optimisation without human oversight.

## Details of the Approach
The strategy evolved over ten rounds and continues through Week 13:
- Weeks 1–3: Broad exploration of the input space
- Weeks 4–6: Identification of ridges, basins, and plateaus
- Weeks 7–10: Trust-region exploitation and stabilisation
- Weeks 11–13: Convergence confirmation and final lock-in

Decisions were informed by observed trends rather than explicit surrogate modelling.

## Performance
Performance was assessed per function using raw objective values, relative improvement over iterations, and stability of results near convergence.

## Assumptions and Limitations
### Assumptions
- Local smoothness near optima
- Informative feedback from small parameter changes
- Stationary objective functions

### Limitations
- Sparse data limits uncertainty estimation
- Manual decision-making introduces subjectivity
- Uneven sampling biases later conclusions

## Ethical Considerations
Transparency is prioritised through complete logging of queries, outputs, and decision rationales to support reproducibility and responsible reuse.
