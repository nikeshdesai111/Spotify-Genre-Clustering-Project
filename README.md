# 🎵 Large-Scale Spotify Track Analysis, Embeddings & Clustering

## 1. Project Motivation & Big Picture
Music recommendation systems rely on identifying meaningful similarity between tracks beyond surface-level genre labels. Spotify provides rich **audio-level features** and **metadata**, but the challenge lies in transforming this high-dimensional, heterogeneous data into representations that meaningfully capture musical structure.

This project investigates how **unsupervised learning**, **dimensionality reduction**, and **representation learning** can be used to uncover latent patterns in Spotify tracks. Rather than predicting a predefined label, the focus is on **discovering structure** in the data and evaluating whether this structure aligns with intuitive musical concepts such as energy, mood, tempo, and stylistic similarity.

At a high level, the project answers the question:

> *Can we group songs in a meaningful way using only data-driven representations, without relying on explicit genre labels?*

---

## 2. Dataset Description
The dataset consists of a **large-scale collection of Spotify tracks**, where each observation corresponds to an individual song. The data includes:

### 2.1 Audio Features
Numerical attributes computed directly from the audio signal, such as:
- Danceability
- Energy
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Liveness
- Valence
- Tempo

These features capture *how a song sounds*, rather than how it is labeled.

### 2.2 Metadata
Additional information about each track, including:
- Popularity
- Duration
- Artist-level identifiers
- Track-level identifiers
- Optional genre or categorical information (when available)

The dataset is high-dimensional, noisy, and heterogeneous — making it well-suited for exploratory and unsupervised analysis.

---

## 3. Data Cleaning & Preprocessing
Before modeling, the dataset undergoes careful preprocessing to ensure statistical validity and computational stability.

### 3.1 Missing Values
- Rows with critical missing audio features are removed
- Non-essential missing metadata fields are handled conservatively

### 3.2 Data Type Validation
- Numerical features are explicitly cast to numeric types
- Non-numeric columns are isolated or dropped when not relevant to modeling

### 3.3 Feature Scaling
Because clustering and PCA are distance-based methods:
- All continuous features are standardized
- This prevents features like loudness or tempo from dominating similarity calculations purely due to scale

---

## 4. Feature Engineering & Selection
Not all raw features are equally informative for clustering.

### 4.1 Feature Subset Construction
- Focus is placed on **audio features** that describe musical characteristics
- Redundant or highly correlated features are evaluated
- Metadata fields not useful for similarity learning are excluded

### 4.2 Motivation
The goal is to create a feature matrix where:
- Each row = a song
- Each column = a meaningful musical dimension
- Distances between rows correspond to perceptual similarity

---

## 5. High-Dimensional Challenges
With many continuous features, the data exists in a high-dimensional space where:
- Distances become less interpretable
- Visualization becomes impossible
- Noise can obscure structure

This motivates dimensionality reduction.

---

## 6. Dimensionality Reduction with PCA
**Principal Component Analysis (PCA)** is applied to transform the feature space.

### 6.1 Why PCA?
- Reduces dimensionality while preserving variance
- Produces orthogonal components
- Enables visualization and noise reduction

### 6.2 Interpretation
- Each principal component represents a linear combination of original features
- Leading components often capture concepts like:
  - Overall energy / intensity
  - Rhythm and tempo
  - Acoustic vs electronic structure

### 6.3 Explained Variance Analysis
- The cumulative explained variance is analyzed
- A small number of components capture a large share of the total variance
- This validates the presence of low-dimensional structure in music data

---

## 7. Clustering Methodology
After dimensionality reduction, multiple clustering techniques are applied to identify latent groupings.

---

## 8. K-Means Clustering
### 8.1 Algorithm Overview
K-Means partitions tracks into *K* clusters by minimizing within-cluster variance.

### 8.2 Implementation Details
- K-Means is applied on PCA-reduced data
- Multiple values of *K* are explored
- Initialization randomness is controlled for reproducibility

### 8.3 Interpretation
- Each cluster centroid represents a prototypical “song profile”
- Clusters often correspond to:
  - High-energy dance music
  - Acoustic or low-tempo tracks
  - Balanced, mid-energy songs

### 8.4 Strengths & Limitations
**Strengths**
- Simple and interpretable
- Efficient at large scale

**Limitations**
- Requires pre-specifying *K*
- Assumes spherical clusters
- Sensitive to outliers

---

## 9. Density-Based Clustering with DBSCAN
### 9.1 Motivation
Music data may not form spherical clusters. DBSCAN allows:
- Arbitrary cluster shapes
- Explicit identification of outliers

### 9.2 Algorithm Overview
DBSCAN groups points based on density:
- Dense regions form clusters
- Sparse points are labeled as noise

### 9.3 Results
- DBSCAN identifies tight, stylistically coherent clusters
- Rare or niche tracks are flagged as outliers
- This reveals musical diversity that K-Means smooths over

---

## 10. Visualization & Exploratory Analysis
### 10.1 PCA Scatter Plots
- Tracks are visualized in 2D PCA space
- Color-coded by cluster assignments
- Clear separation patterns emerge

### 10.2 Cluster Profiling
- Feature distributions are examined within each cluster
- This helps interpret *what makes clusters distinct*

---

## 11. Embedding-Based Extensions (If Applicable)
Beyond raw audio features, the project explores **representation learning** ideas:
- Text-based embeddings from track or artist names
- Learned representations that capture semantic similarity
- Comparison between audio-based and embedding-based groupings

This demonstrates how **modern ML representations** can complement traditional feature engineering.

---

## 12. Evaluation Philosophy
Because this is an unsupervised project:
- There is no single “correct” answer
- Success is measured by:
  - Interpretability
  - Consistency
  - Alignment with musical intuition
  - Stability across methods

---

## 13. Technical Stack
- **Python**
- **Pandas / NumPy** — data handling
- **Scikit-learn** — PCA, K-Means, DBSCAN
- **Matplotlib / Seaborn** — visualization
- **Jupyter Notebook** — iterative experimentation

---

## 14. Project Structure
Spotify_Project_Code.ipynb 
- Full analysis, modeling, and visualization in the notebook

---

## 15. Key Takeaways
- Spotify audio features contain rich, discoverable structure
- Dimensionality reduction reveals meaningful musical axes
- Unsupervised clustering can recover intuitive groupings
- Density-based methods highlight niche and outlier tracks
- Data-driven similarity does not require explicit genre labels

---

## 16. Future Work
- Integrate deep audio embeddings
- Build a recommendation engine using cluster similarity
- Incorporate temporal listening behavior
- Evaluate cluster stability across datasets
- Extend to supervised downstream tasks

---

## 17. Author
**Nicky Desai**  
MSE Data Science | Applied Machine Learning | Statistical Modeling

