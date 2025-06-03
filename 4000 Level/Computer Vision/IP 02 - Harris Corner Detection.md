
### A. Report
![[CV_IndividualProject_02_S19355.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/FeatureDetection%26Matching/test.ipynb)

1. **Image Loading & Preprocessing**:
	
    - Reads a chessboard image (`chessboard.jpg`)
    - Converts it to grayscale (corner detection works on single-channel images)
    - Converts pixel values to float32 format (required by Harris detector)

2. **Corner Detection**:
	
    - `cv.cornerHarris()` applies the Harris algorithm with:
        - `blockSize=2` (neighborhood size for corner detection)
        - `ksize=3` (Sobel kernel size for gradient calculation)
        - `k=0.04` (empirical constant for corner response calculation)

3. **Post-Processing**:
	
    - Dilates the result (`cv.dilate()`) to make detected corners more visible (optional)
    - Marks corners in red by thresholding (`dst > 0.01 * dst.max()` selects strongest responses)

4. **Visualization**:
	
    - Creates a side-by-side comparison:
        - Left: Original RGB image
        - Right: Image with detected corners (red dots)
    - Uses Matplotlib for display with proper BGR-to-RGB conversion

### C. Key Improvements for Basic Algorithm

|**Improvement**|**Purpose**|**Implementation**|
|---|---|---|
|**Gaussian Blur + Histogram Equalization**|Reduces noise and enhances contrast for better detection|`cv.GaussianBlur()` + `cv.equalizeHist()`|
|**Adjusted Harris Parameters**|Improves corner sensitivity|`blockSize=3`, `ksize=5`, `k=0.06`|
|**Non-Max Suppression + Thresholding**|Eliminates weak responses|`cv.threshold()` + `dst[dst < 0.01*dst.max()] = 0`|
|**Sub-Pixel Refinement**|Achieves higher accuracy (up to 0.1px)|`cv.cornerSubPix()` with termination criteria|
|**Centroid Visualization**|Distinguishes initial (red) vs. refined (green) corners|`cv.connectedComponentsWithStats()`|

### D. Applications

1. **Image Stitching (Panoramas)**  
    _Example_: Matching corners across overlapping images to align them.

2. **Object Tracking**  
    _Example_: Tracking vehicle corners in autonomous driving videos.

3. **3D Reconstruction**  
    _Example_: Using corner correspondences from multiple views to build 3D models.

### E. Challenges & Improvements

| **Challenge**              | **Improvement**                                    |
| -------------------------- | -------------------------------------------------- |
| Sensitivity to noise       | Use Gaussian blur (`cv.GaussianBlur()`)            |
| Poor contrast handling     | Apply histogram equalization (`cv.equalizeHist()`) |
| Coarse corner localization | Sub-pixel refinement (`cv.cornerSubPix()`)         |
| Redundant corner detection | Non-maximum suppression + thresholding             |
| Parameter tuning           | Adaptive thresholding based on image stats         |

### F. Questions with Answers

1. **Q: Why does Harris use eigenvalues of the auto-correlation matrix?**  
    _A_: To distinguish corners (both λ large), edges (one λ large), and flat regions (both λ small). _Example_: A checkerboard corner has high λ₁ and λ₂.

2. **Q: What is the purpose of the `k` parameter in the Harris response?**  
    _A_: It controls edge suppression; typical values (0.04–0.06) balance corner/edge sensitivity.

3. **Q: How does non-maximum suppression improve results?**  
    _A_: Retains only local maxima in corner response, eliminating duplicates. _Example_: In dense textures, keeps only the strongest corners.

4. **Q: Why use sub-pixel refinement?**  
    _A_: Corners are often between pixels; refinement achieves 0.1px accuracy for tasks like camera calibration.

5. **Q: What preprocessing steps enhance Harris detection?**  
    _A_: Gaussian blur (reduces noise) + histogram equalization (improves contrast). 
    *Example*: Helps detect corners in low-light images.