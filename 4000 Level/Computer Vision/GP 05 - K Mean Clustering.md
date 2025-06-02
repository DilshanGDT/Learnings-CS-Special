
### A. Report
![[GP_05_Report_YOLO.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/K-MeansClustering/K-Mean.ipynb)

This code performs **K-means clustering** on the **Iris dataset**, evaluates the optimal number of clusters, and measures clustering performance. Here’s a breakdown of the key steps:

1. **Data Loading & Preprocessing
	
	- `pd.read_csv()`: Loads the Iris dataset (sepal/petal measurements and species labels).
	- `StandardScaler()`: Scales the features to have zero mean and unit variance, ensuring equal weight in clustering.
	
2. **Determining Optimal Clusters (`k`)
	
	- **Elbow Method**: Computes *Within-Cluster Sum of Squares (WCSS)* for `k=2` to `10`.
	    - `kmeans.inertia_`: Measures how tightly points are grouped within clusters.
	    - The "elbow point" (where WCSS plateaus) suggests a good `k`.
		
	- **Silhouette Score**: Evaluates cluster separation (higher = better).
	    - `silhouette_score()`: Ranges from -1 (poor) to +1 (well-separated clusters).
	    
	- **Optimal `k`**: Chosen as the value with the **highest silhouette score** after the elbow point.
	
3. **Clustering with Best `k`
	- `KMeans()`: Fits K-means with the optimal `k` and assigns clusters.
	- `fit_predict()`: Returns cluster labels for each data point.
	
4. **Visualization (PCA for 2D Plotting)
	- `PCA(n_components=2)`: Reduces 4D data to 2D for visualization.
	- `plt.scatter()`: Plots clusters, colored by assigned labels.
	
5. Performance Evaluation
	
	- (A) Silhouette Score - Measures *cluster cohesion vs. separation* (higher = better).
		
	- (B) Accuracy (vs. True Labels)
		- `pd.factorize()`: Converts species names (e.g., "setosa") to numeric labels.
		- **Confusion Matrix**: Counts how many points in each cluster belong to each true species.
		- `linear_sum_assignment()`: Finds the best mapping between clusters and true labels.
		- **Accuracy**: Computes how well clusters match true species (only possible with labeled data).
	
### C. Key Parameters & Functions

|**Function/Parameter**|**Purpose**|
|---|---|
|`n_clusters` (KMeans)|Number of clusters (`k`) to form.|
|`random_state=42`|Ensures reproducibility of results.|
|`n_init=10`|Runs K-means 10 times with different initial centroids to avoid local optima.|
|`silhouette_score()`|Quantifies cluster quality (-1 to +1).|
|`PCA(n_components=2)`|Reduces dimensionality for visualization.|
|`linear_sum_assignment()`|Solves the "cluster-to-true-label" matching problem optimally.|
### D. Outputs

1. **Elbow Plot**: Helps visually identify a reasonable `k`.
2. **Cluster Visualization**: 2D scatter plot of PCA-reduced data.
3. **Silhouette Score**: Indicates clustering quality (e.g., 0.55 = moderate structure).
4. **Accuracy**: If true labels are known, measures how well clusters align with species (e.g., 0.89 = 89% correct).

### E. Why This Matters

- **Unsupervised Learning**: K-means groups data without prior labels.
- **Model Selection**: Elbow + silhouette scores prevent arbitrary `k` choices.
- **Validation**: Silhouette score is useful for unlabeled data; accuracy requires labels.

### F. Applications of K-means Clustering

1. **Customer Segmentation (Marketing)**
	
    - Groups customers based on purchasing behavior, demographics, or preferences.
    - _Example_: An e-commerce platform clusters users into "budget shoppers," "luxury buyers," and "deal hunters" for targeted ads.

2. **Image Compression (Computer Vision)**
	
    - Reduces image file size by clustering similar pixel colors and replacing them with centroids.
    - _Example_: Converting a 24-bit color image to 8-bit using K-means (fewer colors = smaller file).

3. **Anomaly Detection (Cybersecurity)**
	
    - Identifies outliers (e.g., fraud, network intrusions) as points far from any cluster centroid.
    - _Example_: Detecting unusual credit card transactions by clustering normal spending patterns.

### G. Challenges in K-means Implementation & Improvements

|**Challenge**|**Improvement**|
|---|---|
|**Sensitive to Initial Centroids**|Use **K-means++** initialization to spread centroids smartly.|
|**Assumes Spherical Clusters**|Try **Gaussian Mixture Models (GMM)** for elliptical clusters.|
|**Fixed Number of Clusters (k)**|Use the **Elbow Method** or **Silhouette Score** to determine optimal `k`.|
|**Fails with Non-Linear Data**|Apply **Spectral Clustering** or **Kernel K-means** for complex shapes.|
|**Scalability for Large Data**|Use **Mini-Batch K-means** or **BIRCH** for faster clustering on big datasets.|
### H. Questions with Answers

##### **Q1: Why is K-means sensitive to initial centroid positions? How can this be mitigated?

- **Answer**: Random initialization may lead to suboptimal local minima.
- **Fix**: Use **K-means++**, which selects distant centroids to improve convergence.

##### **Q2: What metric is used in the Elbow Method to determine the optimal `k`?

- **Answer**: **Within-Cluster Sum of Squares (WCSS)**. The "elbow point" (where WCSS plateaus) suggests a good `k`.
- _Example_: If WCSS drops sharply until `k=3` then flattens, `k=3` is optimal.

##### **Q3: How does the Silhouette Score evaluate clustering quality?

- **Answer**: Measures how similar a point is to its own cluster (cohesion) vs. other clusters (separation).
- **Range**: -1 (poor) to +1 (well-separated). A score of 0.6+ indicates strong structure.

##### **Q4: Why is feature scaling important in K-means?

- **Answer**: K-means uses **Euclidean distance**, so unscaled features (e.g., income vs. age) distort clustering.
- _Example_: Scaling ensures `income` (range: 0–100,000) doesn’t dominate `age` (range: 0–100).

##### **Q5: When would K-means fail, and what alternative would you use?

- **Answer**: Fails for **non-spherical** or **varying-density** clusters (e.g., concentric circles).
- **Alternative**: **DBSCAN** (density-based) or **Spectral Clustering** (graph-based).