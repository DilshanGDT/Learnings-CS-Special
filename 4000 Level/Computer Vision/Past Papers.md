### Question 1

#### a. What is the main difference between clustering and classification?

- **Clustering** is **unsupervised** learning: it groups data based on similarity without predefined labels.
    
- **Classification** is **supervised** learning: it assigns labels to data based on a training set with known categories.

- **Supervised Learning Techniques**

|Technique|Description|
|---|---|
|1. **Linear Regression**|Predicts continuous values (e.g., house price) by fitting a straight line.|
|2. **Logistic Regression**|Used for binary classification (e.g., spam vs. not spam).|
|3. **Decision Trees**|Tree-like model for classification or regression.|
|4. **Support Vector Machines (SVM)**|Finds the optimal boundary between classes.|
|5. **K-Nearest Neighbors (KNN)**|Classifies based on the labels of the K closest data points.|

- **Unsupervised Learning Techniques**

| Technique                                        | Description                                                                  |
| ------------------------------------------------ | ---------------------------------------------------------------------------- |
| 1. **K-Means Clustering**                        | Groups data into K clusters based on similarity.                             |
| 2. **Hierarchical Clustering**                   | Builds nested clusters using a tree-like structure (dendrogram).             |
| 3. **Principal Component Analysis (PCA)**        | Reduces dimensionality while preserving variance.                            |
| 4. **DBSCAN (Density-Based Spatial Clustering)** | Clusters based on density; handles noise well.                               |
| 5. **Autoencoders**                              | Neural networks used for unsupervised feature learning or anomaly detection. |

#### b. How can the clustering quality of any partition of the data be measured?

- **Internal Measures**
These do **not** require ground truth labels. They evaluate how well the data has been clustered based on the **intrinsic structure** (cohesion and separation).

|Measure|Description|
|---|---|
|**Silhouette Score**|Measures how similar an object is to its own cluster (cohesion) vs. other clusters (separation). Values range from -1 to 1 (higher is better).|
|**Dunn Index**|Ratio of the smallest inter-cluster distance to the largest intra-cluster distance. Higher values indicate better clustering.|
|**Davies-Bouldin Index**|Average similarity between each cluster and its most similar one. Lower is better.|
|**Calinski-Harabasz Index**|Ratio of between-cluster dispersion to within-cluster dispersion. Higher is better.|
|**Within-Cluster Sum of Squares (WCSS)**|Measures compactness of clusters. Lower is better. Often used with Elbow Method.|

- **External Measures**
These require **true labels** and compare the clustering result to a known ground truth.

| Measure                                  | Description                                                                                                                                                              |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Adjusted Rand Index (ARI)**            | Measures the similarity between two clusterings adjusted for chance. 1 is perfect match.                                                                                 |
| **Normalized Mutual Information (NMI)**  | Measures the amount of information shared between the true and predicted labels. Ranges from 0 to 1.                                                                     |
| **Fowlkes-Mallows Index (FMI)**          | Geometric mean of precision and recall. Higher is better.                                                                                                                |
| **Purity Score**                         | Measures how many points in each cluster belong to the majority true class.                                                                                              |
| **Homogeneity, Completeness, V-Measure** | Homogeneity: each cluster contains only members of a single class; Completeness: all members of a class are in the same cluster. V-Measure is the harmonic mean of both. |

#### c. Challenges in selecting a clustering algorithm

- **No Universal Best Algorithm** – The effectiveness of an algorithm depends entirely on the nature and structure of your data.
- **Unknown Optimal Number of Clusters (K)** – Many algorithms require the number of clusters in advance, which is often not known.
- **Assumptions About Cluster Shapes** – Some algorithms assume spherical or equal-sized clusters, which may not match real data.
- **High-Dimensional Data Issues** – In many dimensions, distance metrics become less meaningful, reducing clustering accuracy.
- **Scalability Limitations** – Some algorithms, like hierarchical clustering, do not scale well to large datasets.
- **Difficult Cluster Interpretability** – Understanding the meaning or validity of clusters without labels can be challenging.
- **Sensitivity to Distance Metrics** – The choice of similarity or distance measure (e.g., Euclidean, Cosine) directly affects the cluster structure.
- **Noise and Outliers** – Algorithms like K-Means are sensitive to outliers, which can distort the clustering.
- **Feature Scaling Requirement** – Many algorithms require normalized or scaled features to work correctly.
- **Initialization Sensitivity** – Some algorithms (e.g., K-Means) produce different results depending on the initial starting points.

#### d. Discuss the major challenges associated with selecting a clustering algorithm and elaborate on the use of distance as a pair-wise similarity measure. 

- Distance measures quantify how similar or dissimilar two data points are:
	- *Euclidean Distance*: Most common; suitable for continuous, normalized data.
	- *Manhattan Distance*: Useful when movement is restricted to grid-like paths.
	- *Cosine Similarity*: Often used in text data; measures angle between vectors rather than magnitude.
	- *Mahalanobis Distance*: Takes data distribution into account.
	
- *Challenges with Distance Measures*:
	- Choice of distance metric affects clustering results.
	- Requires feature scaling.
	- May lose meaning in high dimensions.

#### e. Briefly describe how k-means algorithm works and list its strengths and weaknesses.

K-means is an **unsupervised machine learning algorithm** used for **clustering** data into a specified number of groups (**k**). Here's how it works:

1. **Initialization**: Select _k_ initial centroids randomly.
2. **Assignment Step**: Assign each data point to the nearest centroid (using Euclidean distance).
3. **Update Step**: Recalculate centroids as the mean of all points assigned to each cluster.
4. **Repeat**: Continue steps 2 and 3 until convergence (centroids no longer change significantly or a set number of iterations is reached).

**Strengths of K-means:**
- **Simple and easy to implement**
- **Fast and scalable** to large datasets
- Works well with **spherical, evenly sized clusters**
- Efficient in **low-dimensional spaces**

**Weaknesses of K-means:**
- Requires choosing the number of clusters **k** in advance
- **Sensitive to initial centroids** (can converge to local minima)
- **Not effective for non-spherical or varying-size clusters**    
- **Sensitive to outliers** and noisy data

#### f. When applying the k-means clustering algorithm for a given set of data points, if different starting positions were used for the centers in separate instances, will the algorithm always converge to the same solution? Explain your answer.

**No, the k-means algorithm will not always converge to the same solution** if different starting positions for the cluster centers are used.
##### Why:
K-means is **sensitive to the initial placement of centroids**. Since the algorithm uses a greedy approach to minimize within-cluster variance, it can get stuck in **local minima** depending on the starting positions. As a result, different initializations can lead to **different final clusters**.
##### Solution:
To address this, it's common to run the algorithm multiple times with different initializations (e.g., **k-means++** initialization) and select the best clustering result based on the **lowest total within-cluster sum of squares (WCSS)**.

#### g. If clusters are to be meaningful, they should be invariant to transformations natural to the problem.

##### i) Suggest a method to obtain invariance to displacement and scale changes. Will this work for all cases? 

- **Method**: Normalize the data (e.g., subtract the mean to center it, then divide by standard deviation or use min-max scaling).
	
- **Effect**: Removes displacement (mean) and scales all features uniformly.
	
- **Limitation**: Works well for linear features but may not be effective if the structure of the clusters changes non-linearly with scale or location.
##### ii) What can be done to obtain invariance to rotation?

- **Method**: Use rotation-invariant features (e.g., principal component analysis (PCA) to align data) or use clustering algorithms based on distance measures invariant to rotation (like spectral clustering).
    
- **Effect**: Aligns data along principal axes, reducing sensitivity to orientation.
    
- **Limitation**: PCA may not preserve cluster separability; effectiveness depends on data geometry.

#### h. Difference between Hierarchical & K-means Clustering

|Aspect|**Hierarchical Clustering**|**K-means Clustering**|
|---|---|---|
|**Approach**|Builds a hierarchy of clusters (bottom-up or top-down)|Partitional: divides data into _k_ non-overlapping clusters|
|**Number of Clusters**|Not required in advance (can be chosen after dendrogram)|Must specify _k_ beforehand|
|**Output**|Dendrogram (tree-like structure showing cluster relationships)|Final cluster centroids and assignments|
|**Deterministic?**|Yes (if distance metric and linkage are fixed)|No (results vary with initial centroids)|
|**Scalability**|Computationally expensive (O(n²) or worse)|Efficient and scalable (linear in number of points and clusters)|
|**Cluster Shape**|Can capture complex structures and nested clusters|Prefers spherical, equal-sized clusters|
|**Flexibility**|Supports various linkage methods and distance metrics|Limited by distance metric (usually Euclidean)|
|**Memory Usage**|Higher (due to distance matrix storage)|Lower (no distance matrix needed)|
**In summary**:

- **Hierarchical clustering** is better for smaller datasets and exploring nested cluster structures.
- **K-means** is more suitable for large datasets where speed and scalability are important.

#### i. “Automatically determining the number of clusters has been one of the most difficult problems in data clustering,” comments on the statement

- **True**. It's challenging because:
    
    - No universal metric.
    - Real-world data often doesn't separate cleanly.
    - Solutions include **Elbow method**, **Silhouette analysis**, **Gap statistic**, but they aren't always definitive.

#### j. K-means Example with City Block Distance

**Initial centers**: A1(2,10), A4(5,8), A7(1,2)

|Point|Distance to A1|Distance to A4|Distance to A7|Cluster|
|---|---|---|---|---|
|A1(2,10)|0|5|9|1|
|A2(2,5)|5|6|4|3|
|A3(8,4)|12|7|9|2|
|A4(5,8)|5|0|10|2|
|A5(7,5)|10|5|9|2|
|A6(6,4)|10|6|7|2|
|A7(1,2)|9|10|0|3|
|A8(4,9)|3|2|10|2|

**Clusters after assignment**:
- Cluster 1: A1
- Cluster 2: A3, A4, A5, A6, A8
- Cluster 3: A2, A7

**New centroids**:
- Cluster 1: (2,10)
- Cluster 2: ((8+5+7+6+4)/5, (4+8+5+4+9)/5) = (6, 6)
- Cluster 3: ((2+1)/2, (5+2)/2) = (1.5, 3.5)

- Cluster 1: Initial centroid (1,1), items (A, G), final centroid (1,1.5) 
- Cluster 2: Initial centroid (8,6), items (B, E, F, H), final centroid (8,7). 
- Cluster 3: Initial centroid (20,3), items (C, D) final centroid (20.5,2.5) 

- Cluster 1: Initial centroid (1,1.5), items (A, G), final centroid (1,1.5) 
- Cluster 2: Initial centroid (8,7), items (B, E, F, H), final centroid (8,7). 
- Cluster 3: Initial centroid (20,2.5), items (C, D) final centroid (20.5,2.5)

#### k. Consider two sets of points distributed roughly uniformly on two circles as shown below. Assume the points in each set are distributed densely enough so that the distances between points on the same circle are smaller than the distances between points on different circles. Describe the result of the k-means clustering algorithm on this data.

-  **K-Means Clustering Behavior:**
	
	- K-means attempts to divide data into k clusters by **minimizing the sum of squared Euclidean distances** between points and their **assigned cluster centroids**.
	
	- However, **k-means assumes convex, roughly spherical clusters** (e.g., blobs), which doesn't match the **non-convex ring shapes** in your data.
	
- **What Actually Happens:**
	
	- **K-means will fail to separate the points based on the two circles.**
	    
	- Instead, it will likely divide the data **based on Euclidean distance** — creating clusters that are split **across the circles** (e.g., cutting each ring into halves or sections).
	    
	- This is because k-means places centroids at the **center of mass**, which is inappropriate for ring-shaped (annular) distributions.
	
- **Why It Fails:**
	
	- Points on **opposite sides of the same ring** are far apart in Euclidean space.
	    
	- Points on **different rings** but **closer in space** might be wrongly clustered together.
	    
	- The cluster centroids may even lie **inside the empty space of the rings**, which makes no sense for circular structures.
	
- **Alternative Approaches:**

To correctly identify the two circular clusters, you'd need algorithms that can handle **non-convex shapes**, such as:

| Method                                    | Why It Works                                                                        |
| ----------------------------------------- | ----------------------------------------------------------------------------------- |
| **DBSCAN**                                | Groups points based on density, not centroid distance. Can detect arbitrary shapes. |
| **Spectral Clustering**                   | Uses graph-based similarity, good for non-linear cluster boundaries.                |
| **Agglomerative Hierarchical Clustering** | Can separate non-convex clusters if combined with proper linkage metrics.           |

### Question 2

#### a. How SVM Works

SVM is a **supervised learning algorithm** used for **classification** (and sometimes regression).

- It works by finding the **optimal hyperplane** that best separates data points of different classes.
- The goal is to **maximize the margin**, i.e., the distance between the hyperplane and the **nearest data points** from each class (called **support vectors**).
- For non-linearly separable data, SVM uses **kernel functions** (e.g., polynomial, RBF) to map data into a higher-dimensional space where a linear separator can be found.

#### b. SVM with XOR (non-linearly separable data)
|x₁|x₂|Label|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|
In 2D space, this is **not linearly separable** — no straight line can separate class 0 and class 1.
##### 🔹 Idea Behind the Kernel Trick:
Instead of manually mapping input to higher dimensions, the **kernel trick** allows SVM to compute dot products in a high-dimensional space **without explicitly transforming the data**.

Let’s define a **feature mapping** that mimics this (for intuition):

$\phi(x_1, x_2) = (x_1, x_2, x_1x_2)$

Then the transformed data becomes:

| x₁  | x₂  | x₁·x₂ | Label |
| --- | --- | ----- | ----- |
| 0   | 0   | 0     | 0     |
| 0   | 1   | 0     | 1     |
| 1   | 0   | 0     | 1     |
| 1   | 1   | 1     | 0     |

Now in **3D space**:
- Points with label 1 are at (0,1,0) and (1,0,0)    
- Points with label 0 are at (0,0,0) and (1,1,1)

These **are linearly separable in 3D**, and SVM can now find a separating hyperplane.

#### c. When your data is imbalanced, is SVM a good approach? Explain.
SVM is **not ideal by default** for imbalanced data because it tends to favor the majority class, leading to poor performance on the minority class. However, it can still work well if you:

- **Use class weights** (e.g., `class_weight='balanced'`)
- **Apply resampling techniques** (like oversampling the minority class)
- **Evaluate with proper metrics** (e.g., precision, recall, F1-score)

With these adjustments, SVM can handle imbalanced data effectively.

#### d. Consider the following training data from the categories:

$$
  $\omega_1: (1,1)^T, (2,2)^T, (2,0)^T$  
- 
  $\omega_2: (0,0)^T, (1,0)^T, (0,1)^T$
$$
##### i. Plot the six training points and construct by inspection the weight vector for the optimal hyperplane and the optimal margin. 

1. **Plot the training data points** for two classes:
    - ω₁: (1,1), (2,2), (2,0)
    - ω₂: (0,0), (1,0), (0,1)
    
2. **Construct the optimal separating hyperplane** by inspection and
3. **Determine the weight vector** w\mathbf{w}w and bias bbb that define the optimal margin.

**Step 1: Plot the points

- We label:
	- Class **ω₁** (Positive Class) with red circles:
	    - (1,1), (2,2), (2,0)
	    
	- Class **ω₂** (Negative Class) with blue crosses:
	    - (0,0), (1,0), (0,1)
	
	^ y
	|           • (2,2)
	|       •
	|           o (1,1)
	|     x           • (2,0)
	|     x
	| x
	+---------------------> x
	   (0,0)
	

**Step 2: Inspect the optimal hyperplane

- By observing the points, you can visually separate the two classes with a **diagonal line** that goes between the two clusters.
	
- A good candidate for a separating hyperplane is the line:
	
	x + y = 1.5
	
- This line lies between the point (1,1) in ω₁ and the points (1,0) and (0,1) in ω₂. It **maximizes the distance (margin)** between the nearest points from both classes.

**Step 3: Find the weight vector w

- The general equation of a line (hyperplane in 2D):
	
	$w^Tx+b=0$
	
- For the line x + y = 1.5, we can rewrite it as:
	
	$x + y − 1.5 = 0 ⇒ w = (1,1)^T,  b = −1.5$
	
- This gives us:
	
	- **Weight vector** $w=[1,1]^T$
	- **Bias** b = −1.5

**Step 4: Optimal margin

- The margin is defined as:
	
	$\text{Margin} = \frac{2}{\|\mathbf{w}\|}​$
	
- Since $\|\mathbf{w}\| = \sqrt{1^2 + 1^2} = \sqrt{2}​,$
	
	$\text{Margin} = \frac{2}{\sqrt{2}} = \sqrt{2} \approx 1.41$

##### ii. What are the support vectors?

- **Support vectors** are the **critical data points** in a Support Vector Machine (SVM) algorithm that lie **closest to the decision boundary** (also called the hyperplane). They are the key elements used to define and position the optimal boundary that separates classes in the feature space.

- **Why are support vectors important?**
	
	- They **directly influence the position and orientation** of the separating hyperplane.
	    
	- If you remove a non-support vector, the hyperplane **won’t change**.
	    
	- But if you remove a support vector, the hyperplane **might shift**, because these are the most “informative” points for the classification decision.

#### e. Difference Between Hyperplane and Optimal Margin

|**Term**|**Definition**|
|---|---|
|**Hyperplane**|A decision boundary that separates data points from different classes.|
|**Optimal Margin**|The maximum possible distance between the hyperplane and the nearest data points from any class (support vectors).|

**Explanation:

- A **hyperplane** in SVM is the **line (in 2D)** or **plane (in higher dimensions)** used to separate two classes.  
- For example, in 2D:
    
    $w^Tx+b=0$
    
	This line tries to divide the data so that one class lies on one side and the other class on the opposite side.
    
- The **optimal margin** is the **largest possible gap** between the two classes that the hyperplane can create, while still correctly classifying all training points.

#### f. What Defines a Good or Bad Feature (e.g., edges, corners)?

- **Good Feature:**
	
	- **Distinctive** – easily recognizable (e.g., corners).
	- **Repeatable** – consistently detected under changes (e.g., lighting, rotation).
	- **Robust to Noise** – stable under image noise.
	- **Well-localized** – accurate position.
	- **Invariant** – works across scale/rotation.

- **Bad Feature:**
	
	- Found in flat/low-texture areas.
	- Sensitive to noise or small changes.
	- Not repeatable or distinctive.

- **Example:**  
	- Corners = good (high uniqueness);  
	- Edges = less reliable for matching.

### Question 3

#### a. Main Steps of Harris Corner Detection

1. **Convert image to grayscale** (if not already).
	
2. **Compute image gradients**:
    - Use Sobel operators to compute gradients in the x and y directions:
	    $I_x$​ and $I_y$​.
	
3. **Compute products of gradients**:
    - $I_x^2, I_y^2, I_x I_y$​
	
4. **Apply Gaussian filter** to smooth the gradient products:    
    - $S_{xx} = G * I_x^2$
    - $S_{yy} = G * I_y^2$
    - $S_{xy} = G * I_x I_y$
    
5. **Form the structure matrix (M)** at each pixel:
	
	  $M = \begin{bmatrix} S_{xx} & S_{xy} \\ S_{xy} & S_{yy} \end{bmatrix}$
	  
6. **Compute the Harris response (R)**:
	
    $R = \text{det}(M) - k \cdot (\text{trace}(M))^2$
    where $k$ is a sensitivity parameter (typically $0.04 \leq k \leq 0.06$)
    
7. **Threshold the response R** to find corner candidates.
8. **Apply non-maximum suppression** to refine corner locations.

#### b. Are Harris Corners rotation invariant?

- Yes, **Harris corners are invariant to rotation**.
	
- **Why?**  
	The Harris detector uses the **eigenvalues of the structure matrix**, which depend on **intensity changes** in all directions around a point. These eigenvalues—and the resulting corner response—remain the same even if the image is rotated.
	
	So, the detector can still identify the **same corners** after rotation, making it **rotation-invariant**.  

#### c. SIFT Descriptor Steps

1. **Scale-space extrema detection**:
    - Detect keypoints by finding local maxima/minima in **Difference of Gaussians (DoG)** across multiple scales.
	
2. **Keypoint localization**:
    - Refine keypoint positions by fitting a 3D quadratic function to remove low-contrast or poorly localized points.
    
3. **Orientation assignment**:
    - Assign one or more dominant **orientations** to each keypoint based on local gradient directions, making the descriptor **rotation-invariant**.

4. **Descriptor generation**:    
    - Around each keypoint, compute **gradient magnitudes and orientations** in a local 16×16 region.
    - Divide it into **4×4 subregions** and build an **8-bin orientation histogram** for each, resulting in a **128-dimensional vector**.
	
	This descriptor is **robust to scale, rotation, and moderate affine changes**.

#### d. What image changes that SIFT descriptor invariance to?

- **Scale**: It detects keypoints at multiple scales using a scale-space (DoG), so features remain stable when image size changes.
    
- **Rotation**: It assigns a dominant orientation to each keypoint and rotates the descriptor accordingly, making it rotation-invariant.
    
- **Illumination (partially)**: It uses gradient magnitudes and normalizes the descriptor, reducing sensitivity to lighting changes.
    
- **Affine distortion (partially)**: While not fully affine-invariant, SIFT is somewhat robust due to local gradient patterns, but large affine changes may still affect it.

#### e. Are corners better than edges?

- Yes, **corners are considered better than edges** for feature detection.
	
- ##### Why?
	- Corners have **variation in intensity in both directions**, making them **more distinctive**.
	- **Edges vary in only one direction**, so matching them can be **ambiguous** (e.g., along the edge line).
	- Corners are more **repeatable and robust** under transformations (e.g., rotation, scale).
	
	*In brief:*  
	**Corners are better** because they provide **unique, stable points** that are easier to detect and match accurately.

#### f. Consider the matrix, M, defined at each image point with image gradients Ix and ly. M = [ Ix^2 IxIy IxIy Iy^2 ] Could M be used for edge detection and/or Corner detection? Briefly justify your answer.

- Yes, the matrix **M** can be used for **corner detection**, but **not ideal for edge detection alone**.

- *Justification:
	
	- **M** is the **structure tensor (or second-moment matrix)** used in **corner detection algorithms** like **Harris Corner Detector**.
	    
	- It captures **gradient changes** in both **x and y directions** over a region.
	
- *How it helps:
	
	- If both **eigenvalues of M are large** → significant intensity change in both directions → **corner**.
	    
	- If **one eigenvalue is large** → intensity change in one direction only → **edge**.
	    
	- If both are small → **flat region** (no feature).
    
	So, M helps in detecting corners and distinguishing them from edges**, but for pure **edge detection**, simpler gradient-based methods (like Sobel) are more direct.

#### g. Difference between SIFT & Harris


|**Aspect**|**Harris Corner Detector**|**SIFT**|
|---|---|---|
|**Invariance**|Not scale-invariant|Scale and rotation invariant|
|**Feature Type**|Detects corners only|Detects keypoints and computes descriptors|
|**Descriptor**|No descriptor – just detects corners|Uses a 128-dimensional descriptor|
|**Robustness**|Less robust to changes in illumination and viewpoint|More robust to illumination and affine changes|
|**Computation Cost**|Faster and simpler|More computationally expensive|

#### h. In difference images, pixel values greater than zero (or greater than a certain threshold) are thought to reflect moving objects in the scene. However, this does not always have to be the case. There are other factors besides object motion that can cause non-zero values in a difference image. List three such factors.

| **Factor**                    | **Explanation**                                                                                      |
| ----------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Lighting Changes**          | Variations in illumination (e.g., turning on/off lights or sunlight shifts) can change pixel values. |
| **Camera Movement**           | Slight shifts or vibrations of the camera can cause the entire scene to appear different.            |
| **Noise in the Image Sensor** | Random sensor noise can cause pixel intensity fluctuations, especially in low-light conditions.      |

### Question 4

#### a. Motion detection vs Moving object detection

- **Motion Detection**:  
	- Detects **any change in pixels** over time — it signals that **something is moving**, but doesn’t identify what.
	
- **Moving Object Detection**:  
	- Goes further by detecting **and localizing the actual object** that is moving (e.g., person, car) — often involves background subtraction, object segmentation, or tracking.
    
	**In short**:
	- **Motion detection** = detects _that_ motion happened.
	- **Moving object detection** = detects _what_ is moving and _where_.

#### b. Object tracking in Computer Vision

- **Object tracking** in computer vision is the process of **locating and following a specific object** across a sequence of video frames **over time**.
	
- It involves:
	- **Identifying the object** in the initial frame.
	- **Predicting its position** in subsequent frames.
	- **Updating the object's location** even with changes in motion, scale, lighting, or partial occlusion.

#### c. Main components of an object tracking algorithm

The two main components of an object tracking algorithm are:

1. **Object Detection (Initialization):**  
	- Identify and locate the object of interest in the first frame or whenever tracking starts.    
	
2. **Object Tracking (Prediction & Update):**  
	
- Continuously predict the object's new position in subsequent frames and update the tracking based on new observations.

#### d. Optical flow calculation assumptions

- **Brightness Constancy**:  
    The pixel intensity of a point remains constant between consecutive frames.  
    _Why?_ Because optical flow tracks how the same point moves, assuming its brightness doesn’t change helps link pixels across frames.
	
- **Spatial Coherence (Smoothness)**:  
    Neighboring pixels have similar motion (velocity).  
    _Why?_ Real-world motions are usually smooth over small regions, so assuming smooth flow helps solve the otherwise under-constrained problem.
    
- **Small Motion**:  
    The displacement of pixels between frames is small.  
    _Why?_ Optical flow equations are derived using a linear approximation (Taylor series), which is valid only for small movements.

#### e. Differential methods for optical flow

- **Differential methods** for optical flow estimation use the **spatial and temporal derivatives** of image intensity to calculate motion. The main idea is based on the **brightness constancy assumption** and small motion.
	
- *Brief explanation:
	
	- Use the **optical flow constraint equation**:
		
	    $I_x u + I_y v + I_t = 0$
	    
	    where $I_x, I_y$​ are spatial intensity gradients, $I_t$​ is temporal gradient, and $u, v$ are the optical flow components (velocity in x and y).
	    
	- Since this gives **one equation with two unknowns $(u,v)$**, additional constraints are needed:
	    - **Lucas-Kanade method**: Assumes flow is constant in a small neighborhood and solves for u,vu,vu,v using least squares.
	    - **Horn-Schunck method**: Adds a global smoothness constraint to enforce spatial coherence of flow.        
	
	In summary, differential methods estimate optical flow by computing intensity derivatives and solving equations under assumptions of brightness constancy and motion smoothness.

| **Method**             | **Key Idea**                          | **Strength**                   |
| ---------------------- | ------------------------------------- | ------------------------------ |
| Horn-Schunck           | Global smoothness assumption          | Dense flow, smooth results     |
| Lucas-Kanade           | Local window-based least squares      | Fast, good for small motion    |
| Pyramidal Lucas-Kanade | Multi-scale approach                  | Handles large motion           |
| Farnebäck              | Polynomial expansion of neighborhoods | Dense and detailed motion      |
| TV-L1                  | Total variation with L1 data term     | Robust to noise & motion edges |

#### f. What is a descriptor in CV algorithms?

- In computer vision (CV), a **descriptor** is a vector that **summarizes the local appearance** around a keypoint or feature in an image.
	
- **Key points:
	
	- It captures **texture, gradients, or intensity patterns** near a feature point.
	    
	- Descriptors are used for **matching** features between images (e.g., in object recognition or image stitching).
    
- Examples: **SIFT, SURF, ORB**.
	
	Think of a descriptor as a **"fingerprint"** for a feature point, used to find similar points in other images.

#### g. Object Tracking with dynamics

- **Tracking with dynamics** means incorporating a **motion model** that predicts how an object moves over time to improve tracking accuracy.
	
- **The idea:
	
	- Instead of just detecting the object's position frame-by-frame, the tracker **uses past states** (position, velocity, acceleration) to **predict where the object will be next**.
	- This prediction guides the search for the object in the new frame, making tracking more robust to occlusions, noise, or fast movements.
	- Common tools include **Kalman filters**, **Particle filters**, or other Bayesian methods that combine prediction (dynamics) with observations.
	
	**In brief:**  
	Tracking with dynamics uses the object's motion behavior to anticipate its future location, enabling smoother and more reliable tracking over time.

#### h. A motion model that is based on a predictor-corrector mechanism

- A **predictor-corrector motion model** works in two steps:
	
	1. **Predictor step:**  
	    Uses the object's current state (position, velocity) and a motion model (e.g., constant velocity) to **predict the next state** (where the object is expected to be).
		
	2. **Corrector step:**  
	    Updates the prediction by **incorporating the actual measurement** (detected object position) to correct errors and refine the estimate.
	
- This approach is commonly used in **Kalman filters**, balancing prediction and observation for accurate tracking.

#### i. Explain a model/method that can be used to estimate optical flow regardless of the magnitude of motion vectors

##### Model
- A model that can estimate optical flow regardless of motion magnitude is the **Pyramidal Lucas-Kanade method**.
	
- **Brief explanation:
	- It builds an **image pyramid**—multiple scaled versions of the image (from coarse to fine).
	- Starts estimating flow at the **coarsest (lowest resolution) level**, where large motions appear smaller and easier to handle.
	- Then **refines the flow estimates progressively at finer levels**, adjusting for details and larger motions.
	
- This **multi-scale approach** overcomes the small-motion limitation of basic differential methods and can handle large motion vectors effectively.

##### Method
- A method to estimate optical flow regardless of motion magnitude is the **Pyramidal Lucas-Kanade** method.

- **How it Works:
	1. **Image Pyramid**: Downscale images to multiple resolutions.
	2. **Start Coarse**: Estimate flow at the lowest resolution where motion is small.
	3. **Refine Upward**: Upsample and refine flow estimates at each higher resolution.
	4. **Final Estimate**: Reach accurate flow at full resolution.
	
- Why Use It?
	- Handles both **small and large motions**.
	- Efficient and accurate.
	- Commonly used in tracking and motion analysis.

### Question 5

#### a. For each part, design a system that would achieve the expected outcomes using computer vision and briefly explain the components of your system. You may use flow diagrams to indicate the system components. Briefly outline an algorithm for each system. State any assumptions you make. 

##### i) At supermarkets customers can generally choose individual pieces of item like fruits and vegetables. In a typical store such items are placed on a scale to determine the weight. The checker possibly has to identify the product and type in the code to the register. Propose a system to automatically identify the product so that job of the human checker can be simplified. 

- **System Components (Flow Diagram):
	
		[Camera] → [Image Preprocessing] → [Feature Extraction / CNN] → [Product Classification] → [Display Product Info]
	
- **Algorithm**:
	
	1. **Capture Image** using an overhead camera when item is placed on the scale.
	2. **Preprocess** (resize, normalize, remove background).
	3. **Extract Features** using a pre-trained CNN (e.g., MobileNet, ResNet).
	4. **Classify Product** using softmax classifier or fine-tuned deep learning model.
	5. **Display Output**: Show product name & code on screen for cashier.
	
- **Assumptions**:
	
	- Each product class has distinct visual characteristics.
	- A dataset of labeled fruit/vegetable images is available for training.
	- Good lighting & stable background are maintained at the scale area.

##### b) Standard headlights of vehicles shine straight ahead, no matter what direction the vehicle is moving. When going around curves, they illuminate the side of the road more than the road itself making it difficult to drive around curves at night. Suggest a system that can be used to turn the lights according to the bend angle to make the driving at night more easy and safe.

- **System Components (Flow Diagram)**:
	
		[Front Camera / Steering Sensor] → [Lane Detection / Curve Estimation] → [Calculate Turn Angle] → [Control Headlight Servo]
	
- **Algorithm**:
	
	1. **Capture road view** using a front-facing camera.
	2. **Apply Lane Detection** (e.g., Hough Transform or DeepLaneNet).
	3. **Estimate Curve Angle** based on lane curvature or steering wheel angle.
	4. **Adjust Headlight** direction using a servo motor controlled by the system.
	
- **Assumptions**:
	
	- Vehicle has electronic headlight control hardware.
	- Lane lines are visible (well-marked roads).
	- System works in real-time with minimal latency.

#### b. For the description given below, design a system that would achieve the expected outcomes using computer vision algorithms and briefly explain the components of your system. Use a flow diagram to indicate the system components. Briefly outline an algorithm for each system. State any assumptions you make. 

##### An office environment needs an automated "office assistant" that would take voice commands from a given location and reach a designated location to deliver items. Obstacles on the way need to be avoided as it moves within the environment.

- **Objective** : Create an intelligent robot that:
	
	- Takes **voice commands** to identify source and destination.
	- Navigates autonomously to **deliver items**.
	- **Avoids obstacles** using vision-based sensing.
	
- **System Components (Flow Diagram)**:
	
		[Voice Input]
		     ↓
		[Speech Recognition & Command Parsing]
		     ↓
		[Destination Mapping + Path Planning]
		     ↓
		[Live Camera Input]
		     ↓
		[Obstacle Detection & Avoidance]
		     ↓
		[Motor Control & Navigation]
	
- **Algorithm**:
	
	1. **Voice Command Processing**:
		
		- Use a microphone and speech recognition (e.g., Google Speech API) to capture and convert commands like:
		    
    > 	"Deliver documents to meeting room 2"
		    
		- Parse keywords for source and destination.
	
	2. **Destination Mapping**:
		
		- Predefine office layout map with labeled locations.
		- Convert parsed command into navigation goal (e.g., coordinates of _meeting room 2_).
		
	 3. . **Path Planning**:
		- Use algorithms like **A*** or **Dijkstra** to compute the shortest path on the office map.
	    
	 4. **Obstacle Detection**:
		
		- Use **depth camera**, **stereo vision**, or **LiDAR** to identify dynamic/static obstacles.
		- Implement **YOLO** or **SSD** object detection to identify and avoid humans or furniture.
		- Real-time image feed helps update route.
		
	3. **Motion Control**:
		- Based on updated path, send motor signals to turn, move, stop or re-route.
	
- **Assumptions**:
	
	- Office map and room locations are preloaded.
	- Floors are flat and suitable for robot movement.
	- Lighting conditions are good for camera input.
	- Obstacle detection works in real time.
	- The robot has motors, wheels, camera, mic, and onboard computation.

#### c. For each part, design a system that would achieve the expected outcomes using computer vision and briefly explain the components of your system. You may use flow diagrams to indicate the system components. Briefly outline an algorithm for each system. State any assumptions you make. 

##### i. You are assigned the task of developing a vision system for driver assistance. The system should warn a human driver when in danger of colliding with a pedestrian. The system should work during day and night, and also in poor weather conditions such as heavy rain. 

- **System Flow Diagram**:
	
		[Camera (Visible & IR)]  [Radar/LiDAR]
	        ↓                     ↓
	   [Sensor Fusion & Preprocessing]
	                ↓
	     [Pedestrian Detection (CNN)]
	                ↓
	        [Distance Estimation]
	                ↓
	         [Collision Prediction]
	                ↓
	         [Warning System Alert]
	
- **Algorithm Outline**:
	
	1. **Input**: Collect real-time frames using RGB + Infrared (IR) camera + Radar/LiDAR.
	    
	2. **Preprocessing**: Enhance visibility (use CLAHE, denoising, etc.) for poor lighting.
	    
	3. **Pedestrian Detection**: Use YOLOv5 or Faster R-CNN trained on varied weather/night datasets.
	    
	4. **Distance Estimation**: Calculate using stereo vision or Radar depth.
	    
	5. **Collision Risk Calculation**:
	    
	    - If `distance_to_pedestrian < safe_threshold` **AND**
	        
	    - `vehicle_speed` indicates potential collision within reaction time → **Raise alert**.
	        
	6. **Output**: Audio/visual warning to driver.
	
- **Assumptions**:
	
	- The vehicle is equipped with cameras and radar/LiDAR.
	- Weather handling via sensor fusion (visible + IR + Radar).
	- Pre-trained models available for pedestrian detection in varying conditions.

##### ii. You need to sort your holiday photographs and find photos which you are in. Describe a frontal faces of you. 

- **System Flow Diagram**:
	
		[Input Image Collection]
		         ↓
		 [Frontal Face Detection]
		         ↓
		 [Face Feature Extraction (SIFT / Deep Embedding)]
		         ↓
		 [Your Face Reference Comparison]
		         ↓
		[Filtered Photos with Matching Face]
	
- **Algorithm Outline**:
	
	1. **Input**: Load all photos.
	    
	2. **Face Detection**: Use Haar Cascades, Dlib, or MTCNN to detect **frontal faces**.
	    
	3. **Feature Extraction**:
	    - Extract deep features using **FaceNet**, **Dlib ResNet**, or **SIFT descriptors**.
	        
	4. **Face Matching**:
	    
	    - Compare extracted faces with your reference face (you provide a few labeled photos).
	        
	    - Use cosine similarity or Euclidean distance for comparison.
	        
	5. **Output**: Store or display images where a match is found above a threshold.

- **Assumptions**:
	
	- Your frontal face reference is available.
	- All photos are reasonably clear (not heavily blurred).
	- The lighting and angles are mostly frontal or slightly varied.

### General Question

#### a. What is yolo? list down 3 such libraries and explain the use case with one sentence

- **YOLO (You Only Look Once)** is a real-time object detection algorithm that detects and classifies objects in a single pass through a neural network, making it fast and suitable for real-time applications.

|**Library**|**Use Case**|
|---|---|
|**Darknet**|Original YOLO implementation used for training and testing YOLO models.|
|**Ultralytics YOLOv5**|PyTorch-based implementation for real-time object detection in custom datasets.|
|**OpenCV (DNN module)**|Enables running pre-trained YOLO models in lightweight C++/Python applications.|

- These libraries are widely used for tasks like surveillance, autonomous driving, and retail analytics.

#### b. What is Radar/LiDAR?

- **Radar** and **LiDAR** are remote sensing technologies used for object detection and environment mapping, especially in autonomous systems.

|Technology|Stands For|How It Works|Key Use Case|
|---|---|---|---|
|**Radar**|Radio Detection and Ranging|Uses radio waves to detect objects and measure distance, speed, and angle.|Vehicle collision avoidance, speed detection.|
|**LiDAR**|Light Detection and Ranging|Uses laser pulses to create high-resolution 3D maps of surroundings.|Autonomous vehicles, terrain mapping.|

- **Summary**: Radar works well in poor visibility (rain/fog), while LiDAR gives more detailed spatial data in clear conditions.

#### c. What are the difference between object detection & object recognition?

|Feature|**Object Detection**|**Object Recognition**|
|---|---|---|
|**Purpose**|Locate and identify **where** objects are in an image|Identify **what** an object is|
|**Output**|Bounding boxes + class labels|Class label (without location info)|
|**Complexity**|More complex, involves localization + classification|Simpler, only classification|
|**Use Case Example**|Detecting all cars and pedestrians in a street image|Recognizing a car model in a cropped image|
|**Techniques**|YOLO, SSD, Faster R-CNN|CNN, ResNet, VGG|

- **Summary**:
	- **Object Detection** = _"Where and what is the object?"_
	- **Object Recognition** = _"What is the object?"_ (assuming you already know where it is)

