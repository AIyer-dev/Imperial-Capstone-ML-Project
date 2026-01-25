# Notebooks Overview: BBO Weekly Planner & Weekly Replay

This repository includes two Jupyter notebooks that support the Imperial College **BBO capstone** workflow. They are designed to be:

- **Reproducible**: given the same `inputs.txt` / `outputs.txt`, they produce the same suggestions.
- **Transparent**: they show *why* a suggestion was made (predicted mean/std for GP, or the heuristic rule used).
- **Practical**: they work with small data (13 iterations) and mixed function dimensionalities (2D → 8D).

> **Honesty note:** During the capstone, many weekly decisions were made using **interpretable heuristics** (freeze, rollback, trust-region, monotonic push).  
> These notebooks provide (1) a formal surrogate approach (Gaussian Process + acquisition) and (2) a heuristic approach that mirrors the reasoning used in the weekly write-ups. You can use either, or compare both.

---

## 1) `bbo_weekly_planner.ipynb`

### Purpose
A **one-shot planner**: load your full history and generate a *single set of next-week suggestions* for **F1–F8**.

### What it does
1. **Parses history** from:
   - `inputs.txt` (the points you submitted), and
   - `outputs.txt` (the observed objective values returned by the portal).

2. Builds per-function datasets:
   - `X` = submitted input vectors (shape: `n_points × d`)
   - `y` = scalar outputs (shape: `n_points`)

3. Proposes next points in **two ways**:
   - **GP Surrogate + Acquisition**
     - Fits a **Gaussian Process** model per function using scikit-learn.
     - Predicts a **mean** and **uncertainty (std)** for candidate points.
     - Selects the next point by maximising an acquisition function:
       - **EI (Expected Improvement)** (default), or
       - **UCB (Upper Confidence Bound)** (optional).
     - Candidate optimisation is done via **random search** over the unit hypercube.

   - **Heuristic Planner**
     - Implements the same decision rules used in the capstone narrative:
       - **Freeze** if the function appears flat (very low output range).
       - **Rollback** to the best observed point if the most recent query regressed sharply.
       - Otherwise, make a small **trust-region perturbation** around the best point.

4. Outputs a table containing:
   - best value so far per function,
   - GP suggestion + predicted mean/std,
   - heuristic suggestion + rule used.

### When to use it
- You want **one clean set of next-week inputs**.
- You want a quick comparison between **formal BO** and **interpretability-first heuristics**.

---

## 2) `bbo_weekly_replay.ipynb`

### Purpose
A **week-by-week replay & audit notebook**: it reconstructs what a GP/heuristic method would have suggested **at each iteration**, using only the data available up to that week.

This is useful for:
- documenting methodology,
- understanding how decisions could evolve,
- producing tables/figures for write-ups.

### What it does
1. **Parses weekly history**:
   - Converts your full input/output logs into a list of weeks.
   - Each week contains `F1..F8` with:
     - submitted vector `x`
     - observed scalar output `y`

2. For each week `t` (training on weeks `1..t`), it:
   - fits a **GP surrogate** per function,
   - proposes the next-week query for week `t+1` (EI/UCB),
   - records the predicted mean/std at the chosen point,
   - also computes a heuristic suggestion and records the reason.

3. Produces two key tables:
   - **Replay suggestions table**
     - For each function and each week, shows:
       - best value so far,
       - GP suggestion + predicted mean/std,
       - heuristic suggestion + reasoning.
   - **Replay vs actual**
     - Merges the replay suggestions with what you actually submitted,
       so you can compare:
       - what you did,
       - what the model/heuristic would have recommended at the time.

4. Optional exports:
   - You can export the replay tables to CSV for reporting.

### When to use it
- You want to **audit** the decision process across the full capstone.
- You want to include a **methodology appendix** / reproducibility evidence.
- You want to generate a “Week N recommendations” table retroactively.

---

## Inputs & Outputs Expected

Both notebooks assume you have two files (or equivalent copies):

- `inputs.txt`: your submitted query points
- `outputs.txt`: the portal’s returned objective values

### Supported formats
- **Labeled format**:  
  `F3: 0.930000-0.620000-0.880000`
- **Plain vector format** (8 lines per week, in `F1..F8` order repeating):  
  `0.500000-0.500000`

If your files differ, update the regex in the parsing cells.

---

## Notes on Reliability (especially high dimensions)

- In **high dimensions** (F7/F8), a GP with ~10–13 points can be unstable.  
  That’s why both notebooks include the heuristic mode and why random-search acquisitions are used.
- In the **final rounds**, the most defensible strategy is often:
  - **lock in the best observed point**, rather than chasing predicted improvements.

---

## Quick Start

1. Put both notebooks in your repo under `notebooks/`
2. Place `inputs.txt` and `outputs.txt` in the same directory *or* update the paths in the notebook.
3. Run cells top-to-bottom.

---

## Suggested citation in README (optional)

You can describe the approach briefly like this:

> “We used a lightweight black-box optimisation workflow combining (i) per-function Gaussian Process surrogates with EI/UCB acquisition (random-search candidate optimisation), and (ii) interpretable heuristics (freeze/rollback/trust-region) to generate weekly query submissions under a strict evaluation budget.”

