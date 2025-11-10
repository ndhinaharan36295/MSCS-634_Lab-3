# MSCS 634 – Lab 3: Clustering Analysis Using K-Means and K-Medoids

## Overview
This lab explores **unsupervised clustering** using the Wine Dataset from the `sklearn` library.  
Two algorithms were applied and compared:
- **K-Means** (centroid-based)
- **K-Medoids** (medoid-based, implemented via `pyclustering`)

The objective is to analyze how each algorithm partitions the same dataset, evaluate their clustering performance using **Silhouette Score** and **Adjusted Rand Index (ARI)**, and visualize how the resulting clusters differ in structure and positioning.

---

## Steps Performed
1. **Data Loading & Preparation**
   - Loaded the Wine dataset from `sklearn.datasets`.
   - Standardized all features using **z-score normalization** (`StandardScaler`) to ensure consistent scaling.

2. **K-Means Clustering**
   - Implemented with `k=3`, reflecting the known class count.
   - Calculated performance metrics:
     - *Silhouette Score* – measures compactness and separation.
     - *Adjusted Rand Index (ARI)* – compares clusters to true class labels.

3. **K-Medoids Clustering (via pyclustering)**
   - Used the Partitioning Around Medoids (PAM) algorithm.
   - Computed a full **distance matrix** and randomly initialized 3 medoids.
   - Evaluated using the same Silhouette Score and ARI metrics.

4. **Visualization & Comparison**
   - Plotted both clustering results side-by-side using the first two standardized features.
   - Marked cluster centers (K-Means centroids in red, K-Medoids medoids in black).
   - Compared the spatial distribution and shape of the clusters.

---

## Key Results

| Algorithm     | Silhouette Score | Adjusted Rand Index | Cluster Centers |
|----------------|------------------|---------------------|-----------------|
| **K-Means**    | ~0.28–0.32       | ~0.38–0.40          | Computed means  |
| **K-Medoids**  | ~0.23–0.27       | ~0.32–0.35          | Actual samples  |

*(Values may vary slightly depending on random initialization.)*

---

## Observations and Insights

- **K-Means** produced more compact and well-separated clusters. Its centroids represent average positions, which helped capture the spherical nature of the Wine dataset’s feature space.
- **K-Medoids**, while slightly less compact, provided robustness by selecting **actual data points** as centers. This leads to slightly irregular cluster shapes but better resistance to outliers.
- The side-by-side visualization showed that K-Means clusters appeared more symmetric and dense, whereas K-Medoids clusters were somewhat unevenly distributed.

---

## When to Use Each Algorithm

| Scenario | Prefer K-Means | Prefer K-Medoids |
|-----------|----------------|------------------|
| Data type | Continuous, numeric | Mixed or categorical |
| Noise sensitivity | Less robust to outliers | Robust to noise/outliers |
| Performance | Faster on large datasets | Slower but more stable |
| Distance metric | Euclidean | Any (e.g., Manhattan, cosine) |

---

## Challenges and Decisions
- Encountered import issues with `scikit-learn-extra`, which required switching to the `pyclustering` implementation for K-Medoids.
- Ensured numerical stability by standardizing all features before clustering.
- Verified algorithm outputs using both **internal** (Silhouette) and **external** (ARI) validation metrics to cross-check accuracy.
