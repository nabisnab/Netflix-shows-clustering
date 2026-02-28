# Netflix Shows Clustering

Unsupervised clustering of Netflix titles using **K-Means** and **PCA** for exploratory analysis and visualization. This project groups movies and TV shows by numeric features (release year, rating, duration) and projects them into 2D space for an interpretable scatter plot.

---

## Overview

The notebook loads the Netflix catalog, preprocesses key columns, scales numeric features, fits a K-Means model with 3 clusters, and reduces dimensions with PCA to produce a 2D scatter plot where each point is a title and color indicates cluster membership.

**Tech stack:** Python, pandas, scikit-learn (KMeans, StandardScaler, LabelEncoder, PCA), seaborn, matplotlib.

---

## Dataset

- **File:** `netflix_titles.csv`
- **Source:** Netflix titles catalog (e.g. [Kaggle Netflix dataset](https://www.kaggle.com/datasets/shivam2503/netflix-shows))
- **Columns used:**
  - `release_year` — numeric
  - `rating` — categorical (e.g. PG-13, TV-MA), encoded to numeric
  - `duration` — e.g. `"90 min"` or `"2 Seasons"`, converted to a numeric “duration” value

Other columns (e.g. `title`, `type`, `listed_in`, `description`) are available in the dataframe for inspection or future use.

---

## Project Structure

```
Netflix-shows-clustering/
├── README.md
├── netflix_titles.csv      # Netflix catalog data
└── showsis.ipynb           # Main analysis notebook
```

---

## Methodology

### 1. Load & inspect

- Read `netflix_titles.csv` with pandas.
- Inspect `release_year`, `rating`, and `duration`.

### 2. Preprocessing

- **Rating:** Encoded to integers with `sklearn.preprocessing.LabelEncoder` (e.g. PG-13 → 0, TV-MA → 1, …).
- **Duration:**
  - Movies: `"X min"` → integer `X`.
  - TV shows: `"X Season(s)"` → `X * 60` (treated as 60 “minutes” per season).
  - Missing values → `0`.

### 3. Scaling

- Features: `release_year`, `rating`, `duration`.
- `StandardScaler` fit on these columns; same scaling used for clustering and PCA.

### 4. Clustering

- **Algorithm:** K-Means (`sklearn.cluster.KMeans`).
- **Parameters:** `n_clusters=3`, `random_state=42`.
- Cluster labels are stored and used for coloring in the plot.

### 5. Dimensionality reduction

- **PCA** with `n_components=2` on the scaled features.
- Result: 2D coordinates per title for visualization.

### 6. Visualization

- **2D scatter plot** (matplotlib + seaborn):
  - X: first PCA component  
  - Y: second PCA component  
  - Color: cluster label  
- Title: e.g. `"KMeans Clusters of Netflix Titles"`.

*(A 3D scatter plot can be added later by using `PCA(n_components=3)` and a 3D plotting backend.)*

---

## Getting Started

### Prerequisites

- Python 3.8+
- Jupyter (or VS Code / Cursor with Jupyter support)

### Dependencies

Install the packages used in the notebook:

```bash
pip install pandas numpy scikit-learn seaborn matplotlib jupyter
```

Or with a requirements file:

```bash
pip install -r requirements.txt
```

*(Create a `requirements.txt` with the above package names and versions if you want reproducible installs.)*

### Run the notebook

1. Put `netflix_titles.csv` in the same directory as `showsis.ipynb` (or adjust the path in the notebook).
2. Open and run `showsis.ipynb` (e.g. `jupyter notebook showsis.ipynb` or run cells in your editor).

---

## Results

- **Clusters:** Titles are assigned to one of 3 groups based on scaled `release_year`, `rating`, and `duration`.
- **Plot:** 2D PCA scatter plot shows how titles separate by cluster; overlap or separation reflects how much these three features explain the structure in the data.

You can extend the notebook by:

- Trying different `n_clusters` (e.g. elbow method or silhouette score).
- Adding more features (e.g. from `listed_in` or text from `description`).
- Switching to a 3D PCA plot for a 3D view of the same pipeline.

---

## License

Dataset usage should follow the terms of the original Netflix/Kaggle dataset. Code in this repo is provided as-is for learning and experimentation.
