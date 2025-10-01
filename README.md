# Genetic Algorithms on the Dry Bean Dataset

Clustering the **Dry Bean** data with a **Genetic Algorithm (GA)** and comparing it to a **K-Means** baseline.  
This is a notebook-first project that follows a course assignment; the repository includes the original guide and the final report (in Persian).

> This work was completed as part of a course project at **Amirkabir University of Technology (Tehran Polytechnic)**. 

---

## Repository contents

- `01_ga_dry_beans.ipynb` — main notebook (data load → baselines → GA → evaluation).
- `Dry_Bean_Dataset.xlsx` — dataset file used during the assignment (place at repo root).
- `Guide.pdf` — assignment guide (grading/requirements).
- `projectreport.pdf` — final report (Persian, includes method, figures, and results). 
---

## Quick start

1) Make sure you have **Python 3.10+** and Jupyter installed.  
2) Put `Dry_Bean_Dataset.xlsx` in the repository root.  
3) Open **`first.ipynb`** and run top-to-bottom.

> Packages commonly used: `numpy`, `pandas`, `scikit-learn`, `matplotlib`, `seaborn`. If something is missing, install it with `pip install <package>`.

---

## Methods (high-level)

### Baseline — K-Means
- Standard K-Means clustering on the feature space.
- Used as a reference for GA performance and qualitative comparison.  
  (See the “K-Means Clustering” figure section in the report.) 

### Genetic Algorithm (for clustering)
The GA is set up to search for a better clustering configuration than K-Means:

- **Chromosome/encoding:** Each chromosome represents a clustering solution. In this assignment, a chromosome contains **7 genes (one per cluster)**; each gene encodes the **coordinates of a cluster centroid**. This directly maps individuals to full clusterings.
- **Initial population:** Randomly generated solutions of the above form. 
- **Fitness function:** Quality of a chromosome’s clustering measured against the **true classes** (the assignment compares resulting clusters to the ground-truth labels and reports **clustering accuracy** as the objective/primary metric). 
- **Selection:** Rank or tournament-style selection that favors higher-fitness individuals.
- **Crossover:** **One-point crossover** between two parents to produce two children, combining centroid genes from both. 
- **Mutation:** Bit/coordinate mutation with some probability to maintain diversity (applied gene-wise to child individuals).
- **Elitism/loop:** Evaluate fitness → select → crossover → mutate → form the next generation; repeat for a fixed number of generations or until improvement stalls.

> The implementation outline in the report defines helper routines such as `initialize_population`, `fitness_function`, `select_parents`, `crossover`, and `mutate`. 

---

## Results (from the report)

- **Clustering accuracy** (vs. true labels):
  - **Genetic Algorithm:** **0.50**
  - **K-Means:** **0.30**
  
  These values are reported in the comparative analysis section and figures (“True Clustering”, “K-Means Clustering”, “GA Clustering”).

- **Qualitative comparison:** Visualizations in the report show the GA clustering aligning closer to the true partitioning than K-Means under the assignment’s setup. 

> For plots and exact setup details, see the figure panels labeled **4-1**, **4-2**, and **4-3** (“K-Means Clustering”, “GA Clustering”, and “True Clustering”) in `projectreport.pdf`.

---

## How to reproduce

1. Run **`01_ga_dry_beans.ipynb`** as provided to replicate preprocessing, baseline, GA, and evaluation.
2. If you change random seeds, mutation/crossover rates, population size, or generations, you may see different accuracy values (that’s expected with evolutionary search).

---

## Notes, limitations, and next steps

- **Objective choice:** Using **accuracy vs. labels** makes the task semi-supervised; purely unsupervised alternatives include **Silhouette** or **Calinski–Harabasz** as GA fitness. You can try swapping the fitness in the notebook to observe differences.
- **Encoding sensitivity:** Encoding centroids gives GA direct control over cluster positions but can be sensitive to scaling; ensure features are standardized in the notebook before clustering.
- **Future ideas:** Multiple restarts, parameter sweeps (population size, mutation rate), and hybrid runs (K-Means seeding followed by GA refinement).

---

## Acknowledgments

- Course project at **Amirkabir University of Technology (Tehran Polytechnic)**.  
- **Assignment guide**: `Guide.pdf`.  
- **Final report**: `projectreport.pdf` (Persian).
