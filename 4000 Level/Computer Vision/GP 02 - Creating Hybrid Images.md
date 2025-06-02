
### A. Report

![[HybridImages Report.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/HybridImageGenerator/HybridImages.ipynb) - Method 1

1. **Image Preparation**:
	
    - Converts images to float32 for precise calculations
    - Splits color channels (BGR format in OpenCV)

2. **Channel Processing Function** (`process_channel`):
    
    - Takes low and high frequency channels
    - Applies Gaussian blur to extract low frequencies from both images
    - Extracts high frequencies by subtracting blurred version from original
    - Combines low frequencies from one image with high frequencies from another
    - Clips values to 0-255 range

3. **Processing Flow**:
    
    - Processes each color channel (B, G, R) separately
    - Merges processed channels back into BGR format
    - Converts back to uint8 for display

4. **Visualization**:
    
    - Shows low frequencies, high frequencies, and hybrid result
    - Converts BGR to RGB for matplotlib display

### C. Code - Method 2

#### Differences from Method 1:

1. **Parameter Passing**:
    
    - The `process_channel` function now explicitly takes `low_sigma` and `high_sigma` as parameters
    - This makes the function more flexible if different sigma values were needed per channel

2. **Function Definition**:
    
    - The function definition is slightly more explicit about what each blur operation is doing
    - Comments are added to clarify the low-pass and high-pass filtering steps

### D. Common Components in Both Methods

1. **Gaussian Blur for Frequency Separation**:
    
    - `cv2.GaussianBlur` with different sigma values controls what frequencies are kept
    - Larger sigma = more blur = keeping lower frequencies

2. **High-Pass Filtering**:
    
    - Achieved by subtracting blurred version from original (high = original - low)

3. **Hybrid Image Creation**:
    
    - Combines low frequencies from one image with high frequencies from another
    - Simple addition of the filtered components

4. **Image Alignment**:
    
    - Both methods ensure images have same dimensions before processing
    - Uses `cv2.resize` if needed

### E. Example Workflow

For an example with `Man.jpg` (low freq) and `Women.jpg` (high freq):

1. `Man.jpg` is heavily blurred (sigma=5) to keep only low frequencies
2. `Women.jpg` is lightly blurred (sigma=15) and subtracted from original to get high frequencies
3. The blurred `Man.jpg` and high-frequency `Women.jpg` are combined
4. Result: From far away you see the man's face, up close you see the woman's details

##### **Key Parameters

- `low_sigma`: Controls how much low-frequency content is kept from first image
- `high_sigma`: Controls what high frequencies are extracted from second image
- Typical values: low_sigma (5-10), high_sigma (10-20)

Both methods achieve the same fundamental result, with Method 2 being slightly more explicit in its parameter handling. The hybrid effect works best when the two images have similar overall structure (like faces) but different fine details.

### F. Three Applications of Hybrid Images

1. **Art & Visual Perception Studies**
    
    - Used in psychology experiments to study how humans perceive images at different distances.
    - Example: A hybrid image of a smiling/sad face changes interpretation based on viewing distance.

2. **Steganography & Hidden Messaging**
    
    - Embedding subtle messages in images that are only visible when viewed up close.
    - Example: A company logo that reveals a secret message when zoomed in.

3. **Advertising & Branding**
    
    - Creating dynamic posters where the image changes based on viewing distance.
    - Example: A movie poster that shows a character’s face from afar but reveals a key scene when viewed closely.

### G. Challenges & Improvements

|**Challenge**|**Possible Improvement**|
|---|---|
|**Misalignment of image features**|Use facial landmark detection (e.g., dlib) to align key features before blending.|
|**Poor hybrid effect due to weak frequency separation**|Optimize sigma values (`low_sigma`, `high_sigma`) experimentally for better blending.|
|**Color inconsistency between images**|Convert to grayscale or normalize color histograms before processing.|
|**Artifacts in high-frequency components**|Use edge-aware filtering (e.g., bilateral filter) instead of Gaussian blur.|
|**Hybrid effect not visible at intended distances**|Adjust frequency cutoffs (`low_sigma`, `high_sigma`) based on expected viewing distance.|
### H. Questions with Answers

##### **Q1: Why do we use Gaussian blur for low-pass filtering in hybrid images?**

**Answer:**  
Gaussian blur effectively attenuates high frequencies while preserving low-frequency information, making it ideal for separating image components.  
**Example:** Blurring a face image (`sigma=5`) retains the overall shape but removes fine details like wrinkles.

##### **Q2: How is a high-pass filter implemented in hybrid image creation?**

**Answer:**  
A high-pass filter is obtained by subtracting a low-pass filtered (blurred) version from the original image:  
`high_frequencies = original_image - blurred_image`.  
**Example:** Extracting edges and textures from a sharp portrait by removing its blurred version.

##### **Q3: What happens if the `low_sigma` and `high_sigma` values are too similar?**

**Answer:**  
The hybrid effect weakens because frequency separation is insufficient. The low-frequency and high-frequency components may interfere, making the result unclear.  
**Example:** If both sigmas are `10`, the hybrid image may appear as a messy blend rather than a distance-dependent illusion.

##### **Q4: Why might a hybrid image fail when combining two unrelated images (e.g., a cat and a car)?**

**Answer:**  
Hybrid images work best when the two images have similar structural compositions (e.g., faces). Unrelated images lack alignment, causing perceptual confusion.  
**Example:** A cat’s fur texture does not align with a car’s edges, making the hybrid effect ineffective.

##### **Q5: How can we improve the hybrid effect for mobile displays where viewing distance varies?**

**Answer:**

- Adjust `low_sigma` and `high_sigma` based on typical screen sizes.
- Use multi-scale hybrid images (combining multiple frequency bands).
- Test on different devices to ensure the effect works at varying distances.  
    **Example:** A phone ad might need a stronger high-pass filter (`sigma=3`) since users view it closely.

### I. [[Paper - Hybrid Images]]
