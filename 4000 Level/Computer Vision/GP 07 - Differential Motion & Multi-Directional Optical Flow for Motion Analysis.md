
### A. Report
![[Task_01_&_03_Report_Team_YOLO.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/MotionDetection/test.ipynb)

- `cv2.imread()` 
    → Loads the input images for motion analysis.  
    _Used to read two frames to compare for motion._
    
- `cv2.cvtColor(..., cv2.COLOR_BGR2GRAY)`  
    → Converts color images to grayscale.  
    _Simplifies computation by removing color information, focusing only on brightness._
    
- `cv2.absdiff(gray1, gray2)`  
    → Computes pixel-wise absolute difference between two grayscale images.  
    _Highlights regions that have changed between the two frames._
    
- `cv2.threshold(..., cv2.THRESH_BINARY)`  
    → Converts the difference image into a binary image using a threshold.  
    _Identifies pixels with significant change (motion areas) and sets them to white._
    
- `cv2.bitwise_not(thresh)`
    → Inverts the binary image.  
    _Enhances visual contrast by making moving regions dark on a light background._
    
- `cv2.cvtColor(..., cv2.COLOR_BGR2RGB)`  
    → Converts BGR images (used by OpenCV) to RGB (used by Matplotlib).  
    _Ensures colors display correctly when plotted with Matplotlib._
    
- `matplotlib.pyplot` functions 
    → Used to display the original images, motion-detected output, and its inverted form.  
    _Helps visualize and compare input frames with detected motion regions._

### C. Results
#### **Task 01: Differential Motion Analysis**

1. **Normal Implementation**
    
    - Compares two grayscale images using absolute difference + fixed threshold.
    - Works well in **static lighting** with **one moving object**.
    
2. **Multiple Moving Objects**
    
    - Successfully detects **all motion regions** if **lighting and background are consistent**.
    
3. **With Noisy Images**
    
    - Fails under noise; false positives appear due to sensitivity to pixel-level changes.
    - **No preprocessing** (e.g., blur) leads to unreliable results.
    
4. **Low-Light Conditions**
    
    - Performance drops due to **low contrast**; only partial motion detected.
    - Needs **contrast enhancement** for improvement.
    
5. **Lighting Changes**
    
    - Varying illumination causes **inconsistent motion detection**.
    - Fixed thresholds either miss or exaggerate motion.
    - Adaptive methods are needed.
    
6. **Improved Version with Motion Direction**
    
    - Uses **optical flow (Farneback method)** to detect and visualize **motion direction**.
    - Arrows show flow vectors; weak/noisy vectors are filtered out by magnitude threshold.
    
7. **Improved Low-Light Version**
    
    - Applies **CLAHE (contrast enhancement)** + **Gaussian Blur (denoising)** + **adaptive thresholding**.
    - Significantly better results under dark conditions.

#### 🔹 **Threshold Value Guidance**

- **< 20**: Very sensitive (captures noise and light changes).
- **30–50**: Balanced, best for general use.
- **> 70**: Detects only large movements, may miss subtle motion.

**Recommendation**: Start with **30–50**, then adjust based on environment.

#### 🔹 **Adding Motion Direction**

To include direction in motion detection:

1. **Optical Flow (Lucas-Kanade or Farneback)** – Gives pixel-wise motion vectors.
    
2. **Frame Differencing + Contours & Arrows** – Tracks bounding boxes and estimates direction over time.

#### 🔹 **Task 03: Optical Flow Streamline Analysis**

- **Middlebury dataset** used for evaluating optical flow.
- **Streamlines** show direction and **color bars** show magnitude.
	
- **Observation**:
    - In one frame, **right-side building** had more motion (downward).
    - In another, **left-side** had more motion (bottomward).
    
- **Conclusion**: Proper flow field interpretation is crucial.

#### 🔹 **Block Matching Technique**

- Compares **blocks of pixels** between frames to track motion.
- Works by finding **corresponding regions**.
- In the example, **wooden parts** matched easily, possibly leading to **false or excessive motion detection**.
### D. Applications

**1. Surveillance and Security Systems**

- **Intruder Detection:** Detect motion in restricted zones (e.g., at night or in low-light conditions).
- **Multiple Object Tracking:** Monitor several individuals or vehicles at once.
- **Behavior Analysis:** Track direction and speed of movement to detect suspicious activity.

**2. Autonomous Vehicles and Driver Assistance**

- **Obstacle Detection:** Identify moving objects (cars, pedestrians) from video input.
- **Lane Change & Motion Prediction:** Use optical flow to predict motion and avoid collisions.
- **Parking Assistance:** Monitor and track motion around the vehicle.

**3. Video Editing and Post-Production**

- **Motion Stabilization:** Detect and correct shaky footage.
- **Background Replacement:** Use motion data to isolate and replace backgrounds in videos.

**4. Human-Computer Interaction (HCI)**

- **Gesture Recognition:** Track hand/body movement for touchless control systems.
- **Virtual Reality (VR):** Provide real-time tracking for immersive environments.

**5. Sports Analysis and Athlete Monitoring**

- **Player Tracking:** Analyze player movement across the field.
- **Performance Metrics:** Measure speed, direction, and motion patterns.

### E. Challenges & Improvements

| **Challenge**                                | **Explanation**                                                              | **Relevant Improvements / Solutions**                                                                     |
| -------------------------------------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **1. Low-light performance**                 | Poor contrast results in incomplete or missed motion detection.              | - Apply **CLAHE** (Contrast Limited Adaptive Histogram Equalization)  <br>- Use **adaptive thresholding** |
| **2. Image noise**                           | Noisy pixels can cause false motion detection.                               | - Apply **Gaussian Blur** or **Median Filtering** to reduce noise before thresholding                     |
| **3. Fixed threshold sensitivity**           | Fixed thresholds may fail under varying conditions (lighting, motion scale). | - Use **adaptive thresholding** based on local image stats  <br>- Consider **Otsu’s method**              |
| **4. Multiple object detection limitations** | Harder to track motion when many objects are moving in different directions. | - Integrate **optical flow** for motion vector tracking  <br>- Use **object segmentation** techniques     |
| **5. Direction ambiguity**                   | Basic difference methods show where motion occurred, not where it's going.   | - Use **Farneback or Lucas-Kanade optical flow** to get motion vectors                                    |

### F. Exam Questions & Answers

 
 **Q1. What is differential motion analysis and how does it work?**

**Answer:**  
Differential motion analysis detects motion by calculating the **absolute pixel-wise difference** between two consecutive grayscale frames and applying a **threshold** to highlight changes.

**Explanation:**  
This method works well in controlled lighting and static backgrounds but fails under noisy or low-light conditions due to its simplicity and sensitivity to minor pixel changes.

**Q2. What are the limitations of using a fixed threshold in motion detection, and how can it be improved?**

**Answer:**  
A **fixed threshold** may cause under- or over-detection when lighting or noise varies.

**Improvements:**

- Use **adaptive thresholding** (e.g., based on local mean or Gaussian-weighted average).
- Apply **contrast enhancement (CLAHE)** and **noise reduction (Gaussian Blur)** before thresholding.

**Explanation:**  
These techniques dynamically adjust sensitivity based on image content, improving robustness.

**Q3. How does optical flow differ from differential motion analysis in motion detection?**

**Answer:**  
Optical flow computes **pixel motion vectors** across frames, indicating **direction and magnitude**, whereas differential analysis only shows **where** motion occurred without direction.

**Explanation:**  
Optical flow (e.g., **Farneback, Lucas-Kanade**) provides richer information and is suitable for tracking motion paths and velocity estimation.

**Q4. What are the main steps involved in a multi-directional block-matching algorithm for motion analysis?**

**Answer:**

1. Divide the first frame into **small patches (blocks)**.
2. Search corresponding blocks in the second frame within a **defined search area**.
3. Compare using metrics like **Sum of Absolute Differences (SAD)**.
4. Determine motion **direction (horizontal, vertical, diagonal)** and visualize via streamlines.

**Explanation:**  
Block matching is simpler than optical flow and useful in structured environments, but can struggle with occlusion or repetitive textures.

**Q5. How can motion detection be improved in low-light environments?**

**Answer:**
- Apply **CLAHE** to enhance local contrast.
- Use **Gaussian Blur** to suppress noise.
- Use **adaptive thresholding** instead of a fixed one.

**Explanation:**  
These preprocessing steps help highlight motion even when the overall image brightness is low, improving accuracy and reducing false negatives.