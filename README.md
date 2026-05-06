# Contributors
- Syed Wasiq Saifi
- Ali Akbar Hasnain

# DTW-based Contact Pattern Analysis (WT)

This repository contains a Jupyter notebook for computing Dynamic Time Warping (DTW) distances between per-residue contact time series from a wild-type (WT) protein system, followed by clustering and validation of the resulting patterns.

## Notebook: dtw_calculation_WT.ipynb

# 📌 What this project does:

- Load contact time series for two chains (A and B) from CSV files.

- Convert to binary contact states (0 = no contact, 1 = contact) when needed.

- Concatenate chains A and B to form a unified set of residue time series.

- Compute pairwise DTW distances between residues (or trajectories).

- Normalize the distance matrix to make distances comparable and stable.

- Cluster with K-Means on an embedded representation of the distances.

- Validate clustering with metrics such as Silhouette score (and, optionally, Davies–Bouldin via MDS embedding).

- Evaluate and visualize distance structure and cluster assignments.

### The notebook sections are organized as:

- 0 for residue without contacts and 1 for residue with contacts

- concatenating the chain A and B of the WT

- calculation and normalization of the distance matrix

- K-Means clustering with validation

- evaluation of the calculated distances


# Project Structure


- `DTW/`
  - `11-WT/`
    - `contacts_chain_A/`
      - `file1.csv`
      - `file2.csv`
    - `contacts_chain_B/`
      - `file1.csv`
      - `file2.csv`
- `Notebook/`
  - `dtw_calculation_WT.ipynb`
 

### ▶️ How to run

Ensure your data is laid out as shown in Expected project structure.
Setup

python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt


### 🧮 What the notebook produces

- Distance matrix: pairwise DTW distances between residue time series.

- Normalized distance matrix: distances scaled for stability and comparability.

- Clustering results: K-Means labels for each residue/series.

- Validation metrics: Silhouette score (and optionally Davies–Bouldin via MDS embedding).

- Figures: plots for distance structure and cluster quality.


### 🔧 Configuration points (where to customize)

Input root:

base_directory = 'DTW/11-WT'
chain_folders = ['contacts_chain_A', 'contacts_chain_B']


Residue column detection:

residue_columns = [col for col in df.columns if not col.startswith('Frame.')]


DTW implementation & parameters (e.g., windowing, normalization).

Number of clusters (k): tune with Silhouette/Davies–Bouldin to pick a reasonable value.

### ✅ Interpreting results

- Low DTW distance ⇒ two residues have similar contact dynamics.

- Clusters group residues with similar temporal contact patterns.

- Silhouette score near 1.0 = well-separated clusters; near 0 = ambiguous; negative = misassignment.

- Davies–Bouldin (lower is better) requires coordinates; embed distances first (e.g., with MDS).
