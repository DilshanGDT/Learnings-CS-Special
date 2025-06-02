
### A. Report 

![[SkinDetection Report.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/SkinDetectorByChromacity/SkinDetector.ipynb)

##### **1. Chromaticity Calculation (`calculate_xy_chromaticity`)**

- Converts image to float32 and normalizes to [0,1] range
- Calculates the sum of RGB values for each pixel
- Computes chromaticity coordinates:
    - `x = R/(R+G+B)` (Red chromaticity)
    - `y = G/(R+G+B)` (Green chromaticity)
        
- These coordinates are illumination-invariant, focusing only on color information

##### **2. ROI Selection (`select_skin_roi`)

- Uses OpenCV's `selectROI` to let the user select a rectangular skin region
- Returns the selected region of interest (ROI)

##### **3. Skin Statistics Computation (`compute_skin_statistics`)

- Calculates mean and covariance matrix of the chromaticity values from the skin ROI
- Returns:
    - Mean x (Red chromaticity mean)
    - Mean y (Green chromaticity mean)
    - Covariance matrix of the chromaticity distribution
    - All chromaticity points from the ROI (for visualization)

##### **4. Skin Detection (`detect_skin_regions`)

- Computes chromaticity values for the entire image
- Uses Mahalanobis distance to measure how "skin-like" each pixel is:
    - `Mahalanobis distance = sqrt((x-μ)ᵀ Σ⁻¹ (x-μ))`
    - Where μ is the mean vector and Σ is the covariance matrix
        
- Creates a binary mask where pixels with distance < threshold are considered skin

##### **5. Image Processing Pipeline (`process_image`)

1. Loads the input image
2. Lets user select a skin ROI
3. Computes skin statistics from ROI
4. Detects skin regions in full image using Mahalanobis distance
5. Applies morphological operations (opening and closing) to clean up the mask
6. Displays results:
    - Original image
    - Skin mask
    - Final output (mask applied to original)
    - Chromaticity distribution (as a KDE plot)

##### **6.Key Concepts

- **Chromaticity Space**: By normalizing RGB values, we remove intensity information and focus only on color, making the detection more robust to lighting variations.
    
- **Mahalanobis Distance**: A statistical measure that accounts for correlations between variables (here, x and y chromaticity). It's better than Euclidean distance for this task because skin tones form an elliptical cluster in chromaticity space.
    
- **Morphological Operations**: The opening (erosion followed by dilation) and closing (dilation followed by erosion) help remove small noise and fill holes in the detected regions.

### C. Applications

1. **Face Detection & Recognition**
    - Skin detection can help segment faces in images, improving accuracy in face detection and recognition systems.
    - Example: Smartphone face unlock systems may use skin detection to refine face localization.
        
2. **Gesture Recognition & Human-Computer Interaction (HCI)**
    - Detecting skin regions helps track hands and fingers for gesture-based control.
    - Example: Virtual reality (VR) hand tracking or touchless interfaces.
        
3. **Medical & Dermatology Analysis**
    - Skin detection can assist in identifying skin lesions, rashes, or abnormalities in medical imaging.
    - Example: AI-based tools for early detection of melanoma from skin images.
	
### D. Challenges & Improvements

| **Challenge**                                                    | **Possible Improvement**                                                        |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Sensitivity to lighting conditions**                           | Use color normalization (e.g., HSV/YCbCr) instead of RGB chromaticity.          |
| **False positives (non-skin regions with similar chromaticity)** | Combine with texture analysis (e.g., Local Binary Patterns - LBP).              |
| **Poor performance on diverse skin tones**                       | Train on a larger dataset with varied skin tones and use adaptive thresholding. |
| **Noise in the skin mask (holes, small artifacts)**              | Apply better post-processing (e.g., adaptive morphological operations).         |
| **Static thresholding (Mahalanobis distance threshold fixed)**   | Use dynamic thresholding (e.g., Otsu’s method) or machine learning (SVM, CNN).  |
### E. Questions with Answers

##### **Q1: Why is chromaticity used instead of raw RGB values for skin detection?**

**Answer:**  
Chromaticity normalizes RGB values by dividing by the sum (R+G+B), making it illumination-invariant. This helps in detecting skin under different lighting conditions.  
**Example:** A face under sunlight and shadow will have different RGB intensities but similar chromaticity.

##### **Q2: What is the role of Mahalanobis distance in skin detection?**

**Answer:**  
Mahalanobis distance measures how far a pixel's chromaticity is from the mean skin chromaticity, considering covariance (color distribution shape). It helps classify skin vs. non-skin pixels statistically.  
**Example:** A pixel with (x=0.5, y=0.3) may be skin if it falls within the expected distribution.

##### **Q3: How does morphological opening/closing improve skin detection results?**

**Answer:**

- **Opening (erosion → dilation)** removes small noise (false positives).
- **Closing (dilation → erosion)** fills holes in detected skin regions (false negatives).  
    **Example:** A speckled skin mask becomes smoother after these operations.

##### **Q4: What are the limitations of using a fixed threshold for Mahalanobis distance?**

**Answer:**  
A fixed threshold may not work for all skin tones or lighting conditions. Adaptive thresholding (e.g., Otsu’s method) or machine learning (SVM/CNN) can improve robustness.  
**Example:** A threshold of 2.5 may miss darker skin tones if not properly tuned.

##### **Q5: How could this method fail in real-world scenarios, and how can it be improved?**

**Answer:**

- **Failure cases:** Similar-colored objects (wood, sand), extreme lighting, or unusual skin tones.
- **Improvements:**
    - Use additional color spaces (YCbCr, HSV).
    - Incorporate texture features (LBP).
    - Train on a diverse dataset.  
        **Example:** A wooden table might be misclassified as skin due to similar chromaticity.