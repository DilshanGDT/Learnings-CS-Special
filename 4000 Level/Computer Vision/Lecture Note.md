### 1. Introduction

#### a. Image Processing

- **Image Processing
	- Performing basic operations on images.
	- Transformation of images into images.
	- to basically make images better for further processing : Low level processing.

- **Image Analysis & Image Understanding
	- Extracting information from images : Mid level processing.
	- Image understanding : Making decisions based on images.

- **Computer Graphics
	- Computer graphics involves generating and manipulating visual content using computers. It includes everything from 2D and 3D image creation, animation, and rendering to visual simulations. It’s widely used in video games, movies, graphic design, and user interfaces.
	
    ![[Pasted image 20250511191754.png]]

#### b. Computer Vision

- **Computer Vision**:  
	- Computer vision is a field of artificial intelligence that enables computers to interpret and understand visual information from the world (like images or videos). It focuses on tasks like object detection, image classification, facial recognition, and scene understanding.
	
	![[Pasted image 20250511191954.jpg]]

- **Human Vision & Computer Vision
	
	- ##### **Human Vision:**
		1. **Light Reception**: Light reflects off objects and enters the eye through the cornea and lens.
		2. **Image Formation**: The lens focuses light onto the retina at the back of the eye, forming an image.
		3. **Photoreceptor Activation**: The retina has rods and cones that convert light into electrical signals.
		4. **Signal Transmission**: These signals are sent to the brain via the optic nerve.
		5. **Visual Processing**: The brain (especially the visual cortex) interprets the signals to recognize objects, depth, colors, motion, etc.
		6. **Context Understanding**: The brain uses memory, experience, and context to understand what is being seen.
    
	- ##### **Computer Vision:**
		1. **Image Capture**: A camera or sensor captures digital images or video.
		2. **Data Input**: The image is converted into pixel data (usually RGB values) stored in arrays.
		3. **Preprocessing**: Techniques like resizing, filtering, or normalization prepare the image for analysis.
		4. **Feature Extraction**: Important patterns (edges, shapes, colors, textures) are identified using algorithms or deep learning.
		5. **Model Analysis**: Trained models (e.g., CNNs) analyze the image to detect or classify objects, scenes, or actions.
		6. **Interpretation**: The system outputs a result (like identifying a face or detecting a road sign) based on learned patterns.
	
	![[Pasted image 20250511192525.png]]

- **Why is vision so difficult? 
	
	- Inverse problem - The forward process (e.g., image formation via camera projection, blurring, noise) is usually well-defined, but reversing it is ill-posed (no unique solution).
	
	- Ex : Image Deblurring – Recovering a sharp image from a blurred one.
     3D Reconstruction – Estimating 3D structure from 2D images (e.g., depth from stereo or SfM).
    
	- Seek to recover some unknowns given insufficient information to fully specify the solution.

- **Sensing
	- Sensors like cameras capture images by detecting light reflected from objects in the environment and converting it into digital pixel values.
	- ex : A smartphone camera taking a picture of a face for facial recognition.
    
	- Images encode properties of the world by capturing:  
		- Material: different surfaces reflect light uniquely, affecting color and texture in the image.
		- Shape: object contours, edges, and shading give clues about 3D form.
		- Illumination: brightness and shadow patterns reveal lighting conditions.
		- Spatial relationships: object positions and occlusions show relative depth and arrangement

- **Encoding
	- Converting raw sensor data (images/videos) into a digital format that can be processed by a computer.
	- ex : Storing an image as a JPEG file or representing a frame as a 2D array of pixel values.
	
	- Images yield 3D world understanding through: 
		- Geometry: structure-from-motion, depth maps, or stereo vision help infer 3D shape,
		- Texture: surface details provide depth cues and distinguish materials.
		- Motion: object or camera movement helps estimate depth and structure.
		- Identity of object: appearance features help recognize and classify known objects

- **Information Representation
	- Structuring or transforming the visual data into meaningful features or formats for analysis.
	- ex : Extracting edges, key points, or regions of interest (like a bounding box around a car) from an image.
	
	- Representations for stored descriptions should include:
		- Objects: symbolic models, point clouds, meshes, or feature vectors.
		- Their parts: hierarchical structures or part-based models (e.g., face components).
		- Properties: attribute lists (e.g., color, size, material) or feature descriptors.
		- Relationships: graphs or spatial models showing how parts and objects are connected or arranged

- **Algorithms
	- A set of rules or models used to analyze and interpret the image data.
	- ex : Using a Convolutional Neural Network (CNN) to classify whether an image contains a cat or a dog.
	
	- involves developing algorithms and techniques that can enable computers to analyze, manipulate, and interpret images and videos in much the same way as humans do.
	
#### c. Application of CV

- Optical Character Recognition (OCR)
- Digit recognition (e.g., AT&T labs)
- License plate readers
- Fingerprint scanners for login
- Face detection
- Smile detection
- Blink detection
- Driver assistance systems
- Human eye and head tracking
- People/person tracking
- Sports analysis
- Medical and biomedical imaging
- Face recognition
- Pedestrian detection
- Gaze tracking (driver monitoring)
- Ball trajectory tracking (e.g., Tennis, Cricket, Snooker)
- Hawk-Eye systems (Tennis and Cricket)
- Protracer (golf ball trajectory)
- Automatic bone and contrast separation
- 3D medical imaging (MRI, CT)
- Image-guided surgery
- Robotics (e.g., NASA Mars Rover, RoboCup)
- Object recognition in supermarkets (e.g., LaneHawk)
- Motion capture for special effects
- Geospatial mapping (e.g., Bing Maps)
- Gaming (e.g., Microsoft Kinect)
- Surveillance systems

### 2. [[IP 01 - Applications & Trends in CV]]

### 3. [[GP 01 - Skin Detection with Pixel Chromaticity]]

### 4. [[GP 02 - Creating Hybrid Images]]

### 5. Feature Detection and Matching

Feature detection and matching are fundamental techniques in computer vision used to identify and compare important regions (features) in images. These techniques are widely used in image recognition, object tracking, panorama stitching, and 3D reconstruction. 

- *Feature Detection* - Identifies distinct and repeatable points in an image (such as edges, corners, or blobs) that are invariant to scale, rotation, and illumination changes.

	![[Pasted image 20250512112028.png]]

- *Feature Matching* - Compares features between two or more images to find correspondences, allowing tasks like object tracking or image stitching.

	![[Pasted image 20250512112054.png]]

#### a. Image Matching, Local Features & Finding Features

- **Image Matching
	
	- To establish correspondences  between images, the following features can be used:
	
	1. **Specific Locations**:
	    - Distinct points like mountain peaks, building corners, or unique snow patches.
	    - These are typically described by the appearance of pixel patches around the point (e.g., texture, color).
        
	2. **Edges**:
	    - Defined by boundaries, such as mountain profiles against the sky.
	    - Matched based on orientation and local edge profiles (e.g., gradient patterns).

- **Feature Findings 
	- For feature findings two main approaches are discussed:
	
	1. **Tracking Features Across Images**:
	    - Identify features in one image and track them in others using local search techniques like:
	        - _Correlation_: Measures similarity between patches.
	        - _Least squares_: Minimizes alignment errors between patches.
            
	2. **Independent Feature Detection and Matching**:
	    - Detect features (e.g., corners, edges) separately in all images.
	    - Match them based on local appearance descriptors (e.g., SIFT, SURF).
    
- **Invariant Local Features
	- Invariant local features are distinctive points or regions in an image that can be reliably detected and matched even when the image undergoes certain transformations. The goal is to ensure these features remain consistent (i.e., identifiable) across different versions of the same scene under varying conditions.
	
	![[Pasted image 20250512130704.png]]
	
	- *Key Properties
		
		1. **Geometric Invariance**
		    - **Translation Invariance**: The feature remains detectable regardless of its position in the image (shifted left, right, up, or down).
	        
		    - **Rotation Invariance**: The feature can be recognized even if the image is rotated (e.g., a corner point remains a corner at any angle).
	        
		    - **Scale Invariance**: The feature is detectable at different magnifications (e.g., a blob or corner should be found whether the object is near or far).
	
	- *Why is this important?
		- Enables robust matching across images taken from different viewpoints, distances, or orientations.
	    
		- Used in applications like:
		    - **Object recognition** (finding a book on a shelf from different angles).
		    - **Image stitching** (panorama creation where the same scene is captured from slightly shifted positions).
		    - **3D reconstruction** (matching key points in multiple images of the same object).
	
	- *Examples of Invariant Feature Detectors
		
		- **SIFT (Scale-Invariant Feature Transform)** – Finds keypoints invariant to scale and rotation.
		- **SURF (Speeded-Up Robust Features)** – Faster approximation of SIFT with similar invariance properties.
		- **ORB (Oriented FAST and Rotated BRIEF)** – Combines FAST corner detection with rotation-aware descriptors.
	
	- *How It Works:
		
		1. **Detection**: Identify stable keypoints (e.g., corners, blobs) using algorithms like Harris corners, DoG (Difference of Gaussians), or FAST.
		2. **Description**: Assign a descriptor (a numerical "fingerprint") to each keypoint, encoding its local appearance in a transformation-resistant way.
		3. **Matching**: Compare descriptors across images to find correspondences.
	
	- *Advantages
		1. **Locality** → Robust to occlusion/clutter (only visible parts are needed).
		2. **Distinctiveness** → Can identify objects in large databases.
		3. **Quantity** → Hundreds to thousands per image.
		4. **Efficiency** → Fast processing for real-time use.
		5. **Generality** → Works for various features (edges, textures, etc.).
	
	- *Applications
		- Image alignment (panoramas)
		- 3D reconstruction
		- Motion tracking
		- Object recognition
		- Database retrieval
		- Robot navigation
	
#### b. [[Paper - Evaluation of Interest Point Detectors]]

#### c. Local measures of uniqueness & Feature Detection

- **Local Measures of Uniqueness
	
	- **Concept**: When analyzing a small pixel window, a "good" feature is one that is **distinctive** and can be reliably matched across different images.
    
	- **Criteria**:
	    - **Flat region**: No significant intensity changes in any direction (bad candidate).
	    - **Edge**: Large change perpendicular to the edge direction, but no change along the edge (ambiguous for matching).
	    - **Corner**: Significant intensity changes in **all directions** (ideal candidate).
		
	- **Example
		- A checkerboard corner is a good feature because shifting the window in any direction (up, down, left, right) causes a large intensity change.
	
- **Feature Detection via Window Shifts
	
	![[Pasted image 20250512141556.png]]
	
	- **Key Idea**: Measure how much a small window changes when shifted by (u,v)(u,v).
	- **Method**: Compute the **Sum of Squared Differences (SSD)** between the original and shifted window:
		
	    $E(u,v) = (x,y)∈W ∑​ [I(x+u,y+v)−I(x,y)]^2$
		
    - E(u,v)E(u,v) quantifies the "error" caused by the shift.
    - Large E(u,v)E(u,v) in **all directions** → Corner (good feature).
	
	*Example:
	- For an edge, E(u,v)E(u,v) is small if shifted along the edge direction but large if shifted perpendicular to it.

- **Taylor Approximation for Small Motions

	- **Assumption**: If $(u,v)$ is small, the intensity change can be approximated using a **first-order Taylor expansion**:
	    $I(x+u,y+v)≈I(x,y)+u∂I/∂x+v∂I/∂y$
		
	- **Result**: The SSD error simplifies to:
	    $E(u,v)≈∑ (x,y)∈W (u(∂I/∂x)+v(∂I/∂y))^2$
	    
	- This can be rewritten using the **structure tensor** (auto-correlation matrix):
	    $E(u,v)≈[u v]M[u v], where M = ∑ W [Ix2IxIyIxIyIy2]$
		
	- Interpretation - Eigenvalues of MM determine feature type:
	    - **Two large eigenvalues** → Corner.
	    - **One large, one small** → Edge.
	    - **Both small** → Flat region.
		
	- Summary
		1. **Good features** (e.g., corners) exhibit large intensity changes in all directions when the window is shifted.
		2. **SSD error** quantifies uniqueness, and Taylor expansion simplifies computation for small shifts.
		3. **Structure tensor** (MM) eigenvalues classify regions into corners, edges, or flat areas.
		
	- Example Application  
		- The **Harris corner detector** uses this principle to find corners by thresholding the eigenvalues of MM.
	
- **Second Moment Matrix (M)
	
	- The second moment matrix **M** (also called the **structure tensor**) summarizes gradient distributions in a local window:
		
		$M=∑x,yw(x,y)[Ix2IxIyIxIyIy2]$
		
	- **Ix,IyI*: Image gradients (derivatives) in x and y directions.
	- **w(x,y)**: Gaussian weighting window to emphasize central pixels.
	
	- Simplified Case (Horizontal/Vertical Gradients) :
		- If gradients are axis-aligned (e.g., only Ix or Iy​ is non-zero), **M** becomes diagonal:
			
			$M=[λ_1 0, 0 λ_2]$
			
	- λ1​,λ2​: Eigenvalues representing gradient strengths along x and y.
	
	- **Interpreting Eigenvalues
		- Eigenvalues (λ1​,λ2​) classify local regions:

| **Eigenvalues**      | **Region Type** | **Interpretation**                        |
| -------------------- | --------------- | ----------------------------------------- |
| λ1≈0λ1​≈0, λ2≈0λ2​≈0 | Flat            | No intensity change (bad feature).        |
| λ1≫0λ1​≫0, λ2≈0λ2​≈0 | Edge            | Change in one direction only.             |
| λ1≫0λ1​≫0, λ2≫0λ2​≫0 | Corner          | Change in all directions (ideal feature). |
		
- **Key Insight :
	- A good corner requires **both eigenvalues to be large**.
	- If either eigenvalue is close to zero, the region is either flat or an edge.

#### d. Harris Detector Basic Properties

1. **Properties: Corner response is invariant to image rotation**
    - The Harris detector uses gradient-based calculations that don't depend on image orientation.
        
2. **Repeatability rate = number of correspondences /number of possible correspondences**
    - Measures how consistently the detector finds the same corners across transformed images.
        
3. **Invariance to image intensity change?**
    - Mostly invariant to brightness/contrast changes because it relies on derivatives (gradients).
        
4. **Change of scale?**
    - Not scale-invariant (corners may be missed or misplaced at different resolutions).
   
#### d.1. [[Paper - Harris Corner Detection]]

#### d.2. [[IP 02 - Harris Corner Detection]]

#### e. Scale-Invariant Feature Transform (SIFT)

- **SIFT (Scale-Invariant Feature Transform)** is a computer vision algorithm used to detect and describe local features in images.
#### e.1. Descriptors

- **What is a Descriptor?
	- A **descriptor** is a numerical representation (feature vector) that describes the local appearance of a keypoint in an image. It encodes information about the texture, gradient patterns, or other distinctive characteristics around the detected keypoint.
	
- **Key Properties of Descriptors:
	1. **Distinctiveness**: Uniquely identifies a keypoint to differentiate it from others.
	2. **Invariance**: Designed to be robust to transformations like:
	    - Rotation (e.g., SIFT’s orientation normalization)
	    - Scale (e.g., detected at multiple scales)
	    - Illumination changes (e.g., gradient-based normalization)
	3. **Compactness**: Stored as fixed-length vectors (e.g., SIFT uses 128-dimensional vectors).
	
- **Why Do We Use Descriptors?
	
	- Descriptors enable **matching and recognition** by quantifying image regions in a way that is:
		
		1. **Comparable**:
		    - Descriptors allow measuring similarity between keypoints (e.g., using Euclidean distance for SIFT).
		    - Example: Matching a keypoint in Image A to the closest descriptor in Image B.
	        
		2. **Robust to Variations**:
		    - Unlike raw pixels, descriptors remain stable under viewpoint changes, noise, or lighting differences.
		    - Example: SIFT descriptors can match the same object rotated by 30 degrees.
	        
		3. **Efficient for Large Databases**:
		    - Compact vectors enable fast indexing/search (e.g., with FLANN or k-d trees).
		    - Critical for applications like image retrieval or SLAM (Simultaneous Localization and Mapping).
		    
- **Applications of Descriptors
	
	1. **Object Recognition** (e.g., finding a product in a cluttered image).
	2. **Image Stitching** (matching keypoints to align panoramas).
	3. **3D Reconstruction** (triangulating points from multiple views).
	4. **Robotics** (localization and mapping using visual landmarks).
	
- **Without descriptors**, keypoints would just be "interesting points" with no way to compare them across images. Descriptors bridge the gap between detection and practical use.

#### e.2. [[Paper - SIFT ]]

#### e.3. [[GP 04 - SIFT & Harris Corner Detection for Feature Mapping]]

#### f. Data Clustering

- **Data clustering** is an **unsupervised machine learning** technique used to **group similar data points** into clusters based on their **features or patterns**.

#### f.1. [[Paper - Pattern Recognition Letters]]

#### f.2. [[GP 05 - K Mean Clustering]]

#### g. Object Detection & Recognition

- **Object Detection
	
	- **What it does**: Identifies and locates objects in an image/video by drawing **bounding boxes** around them.
	    
	- **Key Features**:
	    - Outputs both **class labels** (e.g., "dog," "car") and **coordinates** of bounding boxes.
	    - Handles **multiple objects** in a single image.
	        
	- **Examples**:
	    - Self-driving cars detecting pedestrians and traffic signs.
	    - Security systems identifying intruders in surveillance footage.
	
- **Object Recognition
	
	- **What it does**: Classifies objects in an image **without localization** (no bounding boxes).
	    - Focuses on answering: _"What is in this image?"_
	        
	- **Key Features**:
	    - Outputs only **class labels** (e.g., "cat," "apple").
	    - Simpler than detection but less precise about object positions.
	        
	- **Examples**:
	    - Photo apps tagging images as "beach" or "mountains."
	    - Medical imaging classifying X-rays as "normal" or "fractured."
	
- **Key Differences

|**Aspect**|**Object Detection**|**Object Recognition**|
|---|---|---|
|**Output**|Bounding boxes + labels|Only labels|
|**Use Case**|Autonomous vehicles, surveillance|Image categorization, sorting|
|**Complexity**|Higher (requires localization)|Lower (classification only)|

- **Popular Methods
	- **Detection**: YOLO (You Only Look Once), Faster R-CNN, SSD.
	- **Recognition**: CNNs (e.g., ResNet, VGG), Vision Transformers (ViT).

#### g.1. [[Paper - Optimal Margin Classifier]]

#### g.2. [[GP 06 - SVM]]

### h. Motion Analysis

#### h.1. What is Motion Analysis?

- Machine to be able to understand the notion of motion.
- **In computer vision** sequence of static frames with appropriate time gap, we see a nice motion.

- Image to Video
	- Each frame now becomes I(x,y) → I(x,y,t)
	- Space and time (Space and time are different dimensions)

- Motion is analyzed at a higher level.
- *Motion is analyzed based on correspondence of pairs of interest points.
- Dynamic image analysis more likely to static analysis when there are small number of images/frames.

#### h.2. Motion Field (Velocity Field) & Optical Flow

##### Motion Field

A **motion field** is a **2D representation** of how **3D objects move** in a scene, as viewed from a camera.

- Each point in the image is assigned a **velocity vector** that describes:
    - **Direction** of motion (where the point is moving),
    - **Speed** (how fast it's moving),
    - And sometimes the **depth or distance** from the observer.
    
- It captures how pixels shift over time due to **object movement** or **camera motion**.
	
- Although it's a 3D motion, it’s visualized in 2D because it’s based on image frames.
	
- **Can be computed even with a small number of images**, such as from a short video clip or a stereo image pair.

##### Optical Flow

**Optical flow** refers to the **apparent motion** of objects or surfaces between two consecutive image frames taken closely in time.

- Requires a **very short time gap** between frames so that **motion is smooth** and small.
    
- Assumes **no major changes** (like lighting or object appearance) between frames.
	
- Computation based on two assumptions : 
	- Observed brightness of any object point is constant over time.
	- Nearby points in the image move in similar manner – velocity smoothness 
	- *If these assumptions are violated, optical flow computation will produce errors 
    
- The goal is to estimate a **motion field** by determining the **direction and speed** of motion for **every pixel** in the image.
    
- However, **optical flow is not always equal to the true motion field** — changes in **illumination or shadows** can affect the flow even if the object hasn’t moved.

	![[Pasted image 20250522195716.png]]
	
	![[Pasted image 20250522195907.png]]
	
- **Optical flow can be used to study a large variety of motions.
	- moving observer and static objects.
	- static observer and moving objects.
	- both moving 
	
	*Optical flow analysis does not result in motion trajectories*
	
- **Motion is usually combination of four basic elements:
	- Translation at constant distance from the observer 
	- Translation in depth relative to the observer 
	- Rotation at constant distance about the view axis 
	- Rotation of a planar object perpendicular to the view axis
	
- **Optical-flow based motion analysis is based on:
	- Translation at constant distance is represented as a set of parallel motion vectors.
	- Translation in depth forms a set of vectors having a common focus of expansion.
	- Rotation at constant distance results in a set of concentric motion vectors.
	- Rotation perpendicular to the view axis forms one or more sets of vectors starting from straight line segments
	
	![[Pasted image 20250522200644.png]]
	
	![[Pasted image 20250522200757.png]]
	
- **Spatial and Temporal derivatives**
	
	Methods to compute derivatives needed in order to estimate optical flow.
	
	- Need to compute the spatial derivatives of an image I at the time t 
		- *Sobel operator 
	
	- The temporal derivative between time t and t + δt
		- *Subtraction between frames at times t and t + δt
	
- **Optical Flow methods**
	
	- Block-based methods 
		- Minimizing sum of squared deference or sum of absolute deference, or,
		- Maximizing normalized cross-correlation 
	 
	- Deferential methods of optical flow estimation 
		- Based on partial spatial and temporal derivatives of the image signal
		
		- Deferential methods
			- Lucas-Kanade method - dividing image into patches and computing a single optical flow on each of them.
			- Horn-Schunck method - optimizing a functional based on residuals from the brightness constancy constraint, and a particular regularization term expressing the expected smoothness of the flow field.
			- Buxton-Buxton method - based on a model recovered from the motion of edges in image sequences
		
	- Discrete optimization methods 
		- The whole space is quantized, and every pixel is labelled, such that the corresponding deformation minimizes the distance between the source and the target image 
		- The optimal solution is often computed through min-cut max-flow algorithms or linear programming
	
- **Fast Optical Flow Estimation**
	
	- Estimates **optical flow** regardless of how large the motion is.
    
	- **Steps:**
	    
	    1. **Subtract** the current frame from the previous to get a **temporal difference image**.
	    2. For **nonzero difference pixels**, consider all **possible motion directions**.
	    3. **Rules:**
	        - If difference is **negative** → move toward **higher luminance** in current frame.
	        - If difference is **positive** → move toward **lower luminance**.
	        
	    4. Apply this in **four directions** (horizontal, vertical, two diagonals).
	    5. Treat directions as **vectors**, **average them** per pixel.
	    6. Then, **average each pixel's flow** with that of its **8 neighbors** to smooth the flow field.
	    
		![[Pasted image 20250522203910.png]]
	
- **Tracking with Dynamics**
	
	- *Concept:
		
		- **Tracking with dynamics** means using knowledge of an object's **past motion** to **predict** its future location, unlike detection which processes each frame **independently**.
		
	- *Detection vs. Tracking:
		
		- **Detection**: Locates objects **anew in every frame**, no context.
		    
		- **Tracking**: Uses **previous motion patterns** to predict the object’s new position, then **updates** it with actual measurements.
	    
	- *Goals of Tracking with Dynamics:
		
		1. **Reduce search area** – only look where the object is likely to be.
		    
		2. **Improve accuracy** – predictions help deal with noisy measurements.
	    
	- *Assumptions*:
		
		- **Motion is continuous** – objects don't teleport.
		- **Camera motion is gradual** – no sudden jumps.
		- **Pose changes smoothly** – between camera and scene.
		
	- *Motion Models Used:
		
		1. **Kalman Filter** – Works well for **linear and Gaussian noise** systems.
		2. **Particle Filter** – Handles **nonlinear** and **non-Gaussian** cases using multiple hypotheses.
		
	- *Mechanism:
		
		- **Predictor-Corrector Loop**:
		    - **Predict** next position based on motion model.
		    - **Correct** it using the actual detection (measurement).

#### h.3. Motion Analysis

Motion analysis studies how objects move in a scene and can be done **with or without detecting specific objects**.

- **Motion field** depends on the objects being tracked (object-dependent).
- **Optical flow** measures motion regardless of object boundaries (object-independent).

When images or video frames are available, motion analysis helps in **object detection and tracking** using methods like **kernel-based tracking**.

- **Object Motion**
	
	- Based on detecting moving objects or their feature points.
	    
	- Assumes:
	    - **Maximum velocity** limits where the object can be.
	    - **Small acceleration** means velocity changes smoothly.
	    - **Common motion** means objects move similarly.
	    - **Mutual correspondence** means each point matches exactly one point in the next frame.
	
	- Image motion analysis, especially object tracking combine two components.
		- **Localization** of objects (e.g., detecting faces).
		- **Trajectory filtering** using motion models to predict and track object paths (e.g., tracking an aircraft)

#### h.4. Differential Motion Analysis

- **Image Subtraction
	
	- Compares two consecutive images (**f1** and **f2**) to detect motion by **subtracting pixel values*. 
		
	- Assumes a **stationary camera**, **static background**, and **constant lighting**.
	    
	- A pixel is marked as **moving** if the **difference exceeds a small threshold (ε)**.
	    
	- Can be based on:
	    - **Raw pixel differences**
	    - **Average gray level in a neighborhood**
	    - **Local texture features**
	
	- Useful to detect any object motion **distinct from the background**.
	
	- Detects motion by comparing differences between consecutive frames.
    
	- May **miss small or slow-moving objects**, especially if background contrast is low.
    
	- Ensures detected changes are **likely due to actual motion**.
		
		![[Pasted image 20250522184740.png]]
	
-  **Cumulative Difference**
	
	- Standard image subtraction **doesn't show motion direction**.
	    
	- A **cumulative difference image** sums the weighted differences between a **reference image (f1)** and all other images in the sequence.
	    
	- **Weight (ak)** emphasizes recent frames to reflect **current motion** better.
	    
	- Helps detect motion over time and **highlights consistent changes**.
	
		![[Pasted image 20250522184845.png]]
	
- **Problems of motion field construction
	
	- When part of object boundary is visible and impossible to determine motion completely.

#### h.5. [[Paper - Object Tracking Using Computer Vision - A Review]]

#### h.6. [[Paper - Optical Flow - Revisiting Lucas-Kanade and Horn-Schunck]]

#### h.7. [[GP 07 - Differential Motion & Multi-Directional Optical Flow for Motion Analysis]]

