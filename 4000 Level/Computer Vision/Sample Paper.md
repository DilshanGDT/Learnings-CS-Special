#### 01. a) Assume you are assigned the task of devising a simple skin color detector for a variety of photographs of people. 

##### i. List the steps you would follow with a justification for each step.

1. **Chromaticity Calculation:** Calculate illumination-invariant chromaticity (x, y) for each pixel.
	- **Justification:** Focuses on color, robust to lighting changes.
2. **ROI Selection:** User selects a skin region.
	- **Justification:** Provides a sample of skin color for training.
3. **Skin Statistics:** Compute mean and covariance of chromaticity in the ROI.
	- **Justification:** Models the central tendency and spread of skin color.
4. **Mahalanobis Distance Detection:** Calculate the Mahalanobis distance of each pixel's chromaticity to the skin mean and threshold it.
	- **Justification:** Statistically measures "skin-likeness," accounting for color distribution.
5. **Processing and Output:** Apply morphological operations to refine the mask and display results.
	- **Justification:** Cleans the mask for better visualization and evaluation.

##### ii. How sensitive is your algorithm to color balance (scene lighting)? 
	
- Method is relies on chromaticity, which helps minimize the impact of brightness changes but can still be affected by lighting conditions.
- *Improvements* - Use color normalization (e.g., HSV/YCbCr) instead of RGB chromaticity.

#### b) Hybrid images are generated by superimposing two images at two different spatial scales. 
##### i) Given a set of sample images, explain the steps to obtain hybrid images.

1. **Prepare Images:** Convert to float, split color channels.
    - **Why:** Enables precise filtering per color.
2. **Process Channels:**
    - Blur both channels (low frequencies).
    - Subtract blurred from original (high frequencies).
    - Combine low from one, high from the other.
    - Clip values.
    - **Why:** Separates and combines image details at different scales.
3. **Reconstruct:** Merge channels back, convert to display format.
    - **Why:** Creates the final viewable hybrid image.
4. **Visualize:** Show low, high, and hybrid results.
    - **Why:** Allows observation of the hybrid effect.

##### ii) Suggest three (03) applications where hybrid images can be used.

1. **Art & Visual Perception Studies**
    - Used in psychology experiments to study how humans perceive images at different distances.
    - Example: A hybrid image of a smiling/sad face changes interpretation based on viewing distance.

2. **Steganography & Hidden Messaging**
    - Embedding subtle messages in images that are only visible when viewed up close.
    - Example: A company logo that reveals a secret message when zoomed in.

3. **Advertising & Branding**
    - Creating dynamic posters where the image changes based on viewing distance.
    - Example: A movie poster that shows a character’s face from afar but reveals a key scene when viewed closely.

#### 02. a) Discuss the main challenges associated with selecting a clustering algorithm

##### Describe anyone of this...
- **How to define a cluster?**  
    A cluster is a group of data points that are more similar to each other than to points in other clusters. The similarity is based on distance or density measures.
    
- **What features should be used?**  
    Relevant features should be chosen based on the problem domain. Features should have meaningful variation and influence the grouping of data. Feature selection may involve domain knowledge or statistical methods.
    
- **Should the data be normalized?**  
    Yes, normalization is usually required when features have different scales. It ensures that all features contribute equally to the distance calculation used in clustering.
    
- **Does the data contain any outliers?**  
    This depends on the dataset. Outliers can be detected using visualization (boxplots, scatterplots), statistical methods (z-score, IQR), or clustering itself. They may distort the cluster formation.
    
- **How do we define the pair-wise similarity?**  
    Pair-wise similarity is usually defined using distance metrics like Euclidean distance, Manhattan distance, cosine similarity, or correlation, depending on the data type and clustering method.
    
- **How many clusters are present in the data?**  
    This can be determined using techniques like the elbow method, silhouette score, gap statistic, or domain knowledge. These methods assess clustering performance for different numbers of clusters.
    
- **Which clustering method should be used?**  
    The choice depends on the data structure and requirements. Examples include:
    - K-Means: for well-separated, spherical clusters.
    - DBSCAN: for arbitrary-shaped clusters and outlier detection.
    - Hierarchical: for nested clusters.
    - GMM: for soft clustering and overlapping clusters.
    
- **Does the data have any clustering tendency?**  
    This can be tested using methods like the Hopkins statistic or visual methods like scatter plots or pair plots. A high tendency indicates that meaningful clusters can be formed.
    
- **Are the discovered clusters and partitions valid?**  
    Validation can be internal (e.g., silhouette score), external (e.g., comparing with ground truth), or based on domain knowledge. Good validation shows that clusters are well-separated and meaningful

#### b) Consider the data set given below and find 3 clusters on them using k-means clustering algorithm. Assume that the initial cluster centroids are defined by A, B and. Provide a graphical representation of the clusters.

![[WhatsApp Image 2025-05-22 at 17.13.30_5b7968cd.jpg]]
#### c) When applying the k-means clustering algorithm for a given set of data points, if different starting positions were used for the centers in separate instances, will the algorithm always converge to the same solution? Explain your answer.

- **No**, the K-means clustering algorithm **will not always converge to the same solution** if different starting positions (initial centroids or local minima) are used in separate runs.
##### Explanation:

1. **K-Means is Sensitive to Initial Centroids**  
    The algorithm starts with randomly chosen centroids (or user-defined ones). Based on these, it assigns points to clusters and recalculates the centroids.  
    If you change the initial centroids, the entire process can lead to **different final cluster assignments**.
    
2. **Local Minima Problem**  
    K-means minimizes the **within-cluster sum of squares (WCSS)**. But it’s a **greedy algorithm**, so it may converge to a **local minimum**, not the global one. Different starting points can lead to different local minima (i.e., different clustering results).
    
3. **Convergence is Guaranteed, But Not Uniqueness**  
    K-means **always converges** after a finite number of steps (when assignments stop changing). However, the **final solution is not guaranteed to be the same** across runs with different initializations.

#### d) If clusters are to be meaningful, they should be invariant to transformations natural to the problem. Suggest a method to obtain invariance to displacement and scale changes. Will this work for all the cases?

**To achieve invariance to displacement and scale in clustering:**

- **Standardize the data** by translating and scaling the axes so that **each feature has zero mean and unit variance**.  
    This removes the effects of differences in units or measurement scales.
    
- This helps ensure that **no single feature dominates** the distance calculations just because it has **larger numerical values**.
    
- **However, this method doesn't always work well**.  
    If the data naturally form **well-separated clusters**, standardizing across the entire dataset may **reduce the contrast between clusters** by compressing natural variances, potentially making clustering less effective.

#### 03. a) Explain how an approximation to the first derivative of an image can be obtained by convolving the image with the kernel [1 −1] for the image specified below:[56 64 79 98 115 126 132 133]

- Convolving with [1 −1] means for each pixel, you subtract the next pixel from the current pixel:
$$
f′(x) ≈ f(x) − f(x+1)
$$

- This gives the rate of change between pixels — the discrete approximation of the **first derivative**.
- We slide the kernel across the image. The result has **one fewer value** than the input (since we're comparing pairs).
	[56−64=−8][64−79=−15][79−98=−19][98−115=−17][115−126=−11][126−132=−6][132−133=−1]

- [-8, -15, -19, -17, -11, -6, -1]
	- Ignoring computing a value for the first and last image pixels
	- Then use absolute values

- Result - [8, 15, 19, 17, 11, 6, 1]
##### Same values but different kernel 

1. [56 64 79 98 115 126 132 133], [-1, 0, 1]
	
	- Value at position 2 = −1×56+0×64+1×79 = −56+0+79 = 23
	- Value at position 3 = −1×64+0×79+1×98 = −64+0+98 = 34
	- Result - [23, 34, 36, 28, 17, 7]

2. Image =
	[[ 10,  20,  30,  40],
	 [ 50,  60,  70,  80],
	 [ 90, 100, 110, 120],
	 [130, 140, 150, 160]], [-1, 0, 1]
	
	- Row 1: [10, 20, 30, 40]
		- At col 1: `-1×10 + 0×20 + 1×30 = -10 + 0 + 30 = 20`
		- At col 2: `-1×20 + 0×30 + 1×40 = -20 + 0 + 40 = 20`
	
	- Row 2: [50, 60, 70, 80]
		- At col 1: `-1×50 + 0×60 + 1×70 = -50 + 0 + 70 = 20`
		- At col 2: `-1×60 + 0×70 + 1×80 = -60 + 0 + 80 = 20`
	
	- Row 3: [90, 100, 110, 120]
		- At col 1: `-1×90 + 0×100 + 1×110 = -90 + 0 + 110 = 20`
		- At col 2: `-1×100 + 0×110 + 1×120 = -100 + 0 + 120 = 20`
	
	- Row 4: [130, 140, 150, 160]
		- At col 1: `-1×130 + 0×140 + 1×150 = -130 + 0 + 150 = 20`
		- At col 2: `-1×140 + 0×150 + 1×160 = -140 + 0 + 160 = 20`
	
	- [[20, 20],
		[20, 20],
		[20, 20],
		[20, 20]]

#### b) Indicate where edges would be detected in the result of a) and state why.

- In the result of a), the values represent the **rate of change** in pixel intensity between neighboring values:
	- [8, 15, 19, 17, 11, 6, 1]
	
- Edges are typically detected at points where this rate of change is **significantly high**, indicating a sudden change in intensity — which usually corresponds to **object boundaries or texture changes** in the image.
	
- The **highest value** is **19**, which occurs between pixel values **79 and 98** — this is the **strongest edge**.
    
- Other significant changes are at **15** (between 64 and 79) and **17** (between 98 and 115), indicating additional potential edges.
	
- Therefore edges would be detected:
	- Between **64 and 79**
	- Between **79 and 98**
	- Between **98 and 115**

#### c) When would detecting corners be more appropriate than detecting edges as an initial step in an application using computer vision?

- Corners are points where **two edges meet**, making them **more informative and unique** than edges alone. They are ideal for:
	
	- **Object recognition** – corners help identify and differentiate specific shapes.
	- **Image stitching / panorama creation** – matching corners helps align overlapping images accurately.
	- **3D reconstruction** – corners provide reliable features to track across multiple views.
	- **Motion tracking** – corners remain consistent and easy to follow over time.

In contrast, edges may be **ambiguous** (e.g., long straight lines) and can’t be uniquely matched across images. Therefore, when **precise localization and feature uniqueness** are required, corner detection is preferred.
##### Madam Answer : 
Detecting corners would be more appropriate when only a sparse set of points are needed, especially facilitating the detection of corresponding points in multiple images. This is used, for example, in motion tracking.

#### d) The Harris corner detection algorithm computes a 2 x 2 matrix at each pixel based on the first derivatives at that point and then computes the two eigenvalues of the matrix. Explain how you can use the two eigenvalues to label each pixel as a locally smoothed region, an edge point, or a corner point.

The **Harris corner detection algorithm** uses a **2×2 structure matrix** (also called the second moment matrix) at each pixel, built from image gradients (first derivatives). The **eigenvalues** of this matrix, denoted as **λ₁** and **λ₂**, describe how intensity changes in different directions around the pixel.
##### Interpretation using eigenvalues:

1. **Flat / Homogeneous Region:**
    - Both eigenvalues are **small**:  
        `λ₁ ≈ 0` and `λ₂ ≈ 0`
        
    - Intensity does **not change much** in any direction.
    - → **Label:** _Locally smoothed (flat) region_
    
2. **Edge:**
    - One eigenvalue is **large**, the other is **small**:  
        `λ₁ >> λ₂` or `λ₂ >> λ₁`
        
    - Intensity changes **in one direction** (strong gradient), but not in the perpendicular direction.
    - → **Label:** _Edge point_
    
3. **Corner:**
    - Both eigenvalues are **large**:  
        `λ₁ >> 0` and `λ₂ >> 0`
        
    - Intensity changes significantly **in both directions** — characteristic of a **corner**.
    - → **Label:** _Corner point_
##### Summary Table:

|λ₁|λ₂|Interpretation|
|---|---|---|
|Small|Small|Flat region|
|Large|Small|Edge|
|Large|Large|Corner|

#### e) Explain the changes SIFT descriptor is robust to. Is it invariant to major view point changes as well?

The **SIFT (Scale-Invariant Feature Transform)** descriptor is designed to be **robust to common image transformations**. It achieves this by detecting keypoints at multiple scales and computing descriptors based on **local gradient orientation histograms**, which makes it:

- **Invariant to**:
    - **Translation**
    - **Rotation**
    - **Scale changes**
    - **Illumination variations**, including brightness shifts and contrast changes

However, **SIFT is not fully invariant to major viewpoint changes** (e.g., large changes in camera angle), as such transformations can significantly alter the local appearance around keypoints.

#### 04. a) What happens when there is no clear Hyperplane in SVM?

##### In such cases, SVM handles this in two main ways:

1. **Soft Margin SVM**:
    - Allows some **misclassifications** by introducing **slack variables**.
    - Finds a hyperplane that balances **maximum margin** and **minimum classification error**.
    - Useful for **noisy or overlapping data**.
    
2. **Kernel Trick**:
    - Transforms the input data into a **higher-dimensional space** where it **may become linearly separable**.
    - Uses **non-linear kernels** (like RBF, polynomial) to separate complex data patterns.

So, when no clear hyperplane exists, SVM adapts by either **allowing some errors** (soft margin) or **transforming the feature space** (kernel trick) to find a better separating boundary.

#### The picture below shows some original data points. In 1-dimensional, this data is not linearly separable. Explain how, after applying the transformation ϕ(x) = x² and adding this second dimension to our feature space, the classes become linearly separable.

![[Pasted image 20250522164031.png]]

#### b) What is this approach called in SVM?

- Lifting’ of the data points represents the mapping of data into a higher dimension. This is known as kernelling.

#### c) Can a similar approach be used for the XOR Problem? Explain

- Yes, a similar approach can solve the XOR problem by transforming the data into a higher-dimensional space.

- In 2D, the XOR points are not linearly separable. But by adding a new feature (e.g., `x₁ * x₂`), we map each point from 2D to 3D:
	
	- Class w₁: (1, 1, 1), (−1, −1, 1)
	- Class w₂: (−1, 1, −1), (1, −1, −1)

- Now, the two classes are linearly separable based on the third feature. A simple hyperplane like `wᵗ = (0, 0, 1), b = 0` can separate them.

- ##### To make the data linearly separable, we **transform** it into a **higher-dimensional space**. In the given answer, each 2D point `(x₁, x₂)` is transformed to a **3D point** by adding a third feature: `x₁ * x₂`.

- So:
	- (1, 1) → (1, 1, 1)
	- (−1, −1) → (−1, −1, 1)
	- (−1, 1) → (−1, 1, −1)
	- (1, −1) → (1, −1, −1)

#### d) When your data is imbalanced, is SVM a good approach?

- When your data is imbalanced, **SVM (Support Vector Machine)** is generally **not the best approach by default** because:
	
	- SVM tries to find a decision boundary (hyperplane) that maximizes the margin between classes.
	- In imbalanced data, the majority class dominates, so the hyperplane may be biased toward the majority class.
	- This results in poor classification performance on the minority class (often the class of interest).

- **However**, SVM can still be used effectively with some adjustments:
	
	- Using **class-weighted SVM**, where higher penalty is assigned to misclassifying minority class samples.
	- Using **different kernel functions** or tuning parameters carefully.
	- Combining SVM with **sampling techniques** (oversampling minority, undersampling majority).
	
- ##### Adjustments
	- - **Data-level:** Oversample/undersample to balance dataset.
	- **Algorithm-level:** Use class weights or cost-sensitive learning.
	- **Evaluation:** Use suitable metrics beyond accuracy.
	
- ##### Other techniques
	
	1. **Tree-Based Methods**
		- **Random Forests**
		    - Robust to imbalance, especially if you tune class weights or use balanced subsampling.
		    
		- **Gradient Boosting Machines (GBM), e.g., XGBoost, LightGBM, CatBoost**
		    - Can handle imbalance via parameter tuning (e.g., scale_pos_weight in XGBoost) and are very flexible.
		
	2. **Ensemble Methods Specifically for Imbalanced Data**
		- **Balanced Random Forest**
		    - Uses balanced bootstrap samples.
		    
		- **EasyEnsemble and BalanceCascade**
		    - Create ensembles by resampling majority class.
		
	3. **Neural Networks**
		- Can be used with class weighting or focal loss to focus learning on minority classes.
		
	4. **k-Nearest Neighbors (k-NN)**
		- Can work if combined with appropriate resampling or distance weighting but may struggle on highly imbalanced data.

#### 05. For each part, design a system that would achieve the expected outcomes using computer vision algorithms and briefly explain the components of your system. Use flow diagrams to indicate the system components. Briefly outline an algorithm for each system. State any assumptions you make. 

#### a) A driver assistant system equipped with a method to monitor how alert a car driver is and sets an alarm when he/she is about to fall asleep. 

**Assumptions:**
- A camera is mounted facing the driver’s face.
- The system can process video frames in real-time.
- Driver fatigue is detected mainly by eye closure and yawning.

**System Components & Flow Diagram:**

	Camera (Driver Face) 
      ↓
	Face Detection Module → Facial Landmark Detection (Eyes, Mouth) 
      ↓
	Eye State & Yawn Detection 
      ↓
	Alertness Assessment Module (Calculate Eye Aspect Ratio, Yawn Frequency) 
      ↓
	If Driver Fatigue Detected → Trigger Alarm (Sound/Vibration)
      ↓
	Output Alarm Signal

**Brief Algorithm:**

1. Capture video frames of the driver’s face continuously.
2. Detect the face using a face detection model (e.g., Haar cascades, MTCNN).
3. Detect facial landmarks to locate eyes and mouth.
4. Calculate **Eye Aspect Ratio (EAR)** to detect eye closure (blink duration and frequency).
5. Detect yawns by monitoring mouth opening over time.
6. If EAR remains below a threshold for a specific time or yawning frequency exceeds a limit, classify driver as drowsy.
7. Trigger alarm to alert the driver.

#### b) A vision system to automatically monitor the speed limit for a vehicle by “reading” any speed limit signs which are passed by the car.

**Assumptions:**
- A camera is mounted facing forward to capture the road.
- System processes video frames in real-time.
- Speed limit signs have known shapes and colors (e.g., circular with numbers).
- The environment allows clear visibility of signs.

 **System Components & Flow Diagram:**

	Forward-Facing Camera 
      ↓
	Speed Sign Detection (Object Detection Model, e.g., YOLO/SSD) 
      ↓
	Speed Sign Segmentation & Extraction 
      ↓
	Optical Character Recognition (OCR) on Extracted Sign 
      ↓
	Speed Limit Value Recognition 
      ↓
	Compare Recognized Speed Limit with Vehicle Speed 
      ↓
	Display/Alert if Speed Exceeds Limit

**Brief Algorithm:**

1. Capture video frames from the forward-facing camera.
2. Use an object detection model trained on traffic signs to detect and localize speed limit signs.
3. Extract the detected sign region from the frame.
4. Preprocess the sign image (grayscale, thresholding) for clearer digits.
5. Use OCR (e.g., Tesseract, CNN-based digit recognition) to read the speed limit number.
6. Compare the recognized speed limit value with the vehicle’s current speed (obtained from speed sensors or GPS).
7. If the vehicle speed exceeds the detected limit, notify the driver via a display or alarm.