### A. Paper
![[Object_Tracking_Using_Computer_Vision_A_Review.pdf]]

### B. Keywords & Explanations

|Keyword|Explanation|
|:--|:--|
|Object Tracking|The process of locating a moving object over time using a camera.|
|Computer Vision|A field of AI that enables computers to "see" and interpret visual data.|
|Image Processing|Techniques used to manipulate and analyze images for feature extraction.|
|Data Association|Methods to link object detections across frames in a video.|
|Deep Learning|A subset of machine learning using neural networks to learn from data.|
|Appearance Model|Uses visual features like edges and corners to identify objects.|
|Multi-Cue|Object tracking using combined image features like color and texture.|
|Monocular Camera|A single camera used to capture images for tracking.|
|Stereo Camera|A camera system with two or more lenses to capture 3D information.|
|RGB-D Camera|A camera that captures both color images and depth information.|
|Hybrid Sensors|Tracking systems that combine different sensor types like cameras and radar.|
|Datasets|Collections of images or videos used to train and test tracking algorithms.|
|Detection and Localization|Identifying and pinpointing object positions in a frame.|
|Tracking by Detection|A two-step tracking method: detect objects, then associate them across frames.|

### C. Brief Summary

**1. Introduction**

- Object tracking in computer vision is crucial for autonomous systems like vehicles, drones, and robots.
- It enables machines to perceive and respond to changes in their environment.
- This review examines methods, tools, and applications to improve object tracking.

**2. Previous Reviews**

- Previous reviews focus on specific areas of object tracking.
    
- This review provides a broader view, comparing different approaches.
    
    - **2.1. Appearance Model:**
        
        - Appearance models use geometric features for object identification.
        - They struggle with changes in object appearance.
            
    - **2.2. Multi-Cue:**
        
        - Multi-cue methods use multiple image cues like color and texture.
            
        - They combine handcrafted features with deep learning.
            
    - **2.3. Deep Learning:**
        
        - Recent reviews focus on deep learning for object tracking.
            
        - Deep learning has shown significant improvements in object detection.
            
    - **2.4. Applications-Based:**
        
        - Some reviews focus on specific applications like ship tracking or long-term tracking.
            
    - **2.5. Trend in Reviews:**
        
        - There's a growing interest in deep learning methods for object tracking.
            
        - This review compares different approaches and considers hardware constraints.
            

**3. Sensor Equipment**

- Object tracking relies on sensor input, and the choice of sensor depends on the application.
    
- The review categorizes vision sensors into monocular, stereo, depth-based, and hybrid.
    
    - **3.1. Monocular Cameras:**
        
        - Monocular cameras are widely used but have limitations in estimating depth.
            
        - Some setups use multiple monocular cameras to overcome this.
            
    - **3.2. Depth-Based Cameras:**
        
        - Depth-based cameras like stereo and RGB-D provide depth information.
            
        - Stereo cameras use two or more monocular cameras.
            
        - RGB-D cameras use infrared to measure depth.
            
    - **3.3. Hybrid Sensors:**
        
        - Hybrid sensors combine different sensors like cameras and radar.
            
        - They are used in applications with complex data requirements, such as autonomous vehicles.
	
**4. Datasets**

- Object tracking datasets are crucial for developing and evaluating tracking methods.
    
- The datasets vary in focus, including autonomous driving, single-object tracking, and multiple-object tracking.
    
    - **4.1. Object Tracking Datasets in Autonomous Vehicles:**
        
        - Datasets like KITTI [35] provide data for autonomous driving research.
            
        - These datasets often include data from various sensors.
            
    - **4.2. Single-Object Tracking Datasets:**
        
        - Datasets are designed for tracking a single object in a video.
    - **4.3. Multiple-Object Tracking Datasets:**
        
        - Datasets focus on tracking multiple objects simultaneously.
            
        - MOT challenge datasets are a key example [45].
            
    - **4.4. Miscellaneous Datasets:**
        
        - Datasets that don't fit into the above categories.
    - **4.5. Recommendations for Dataset Selection:**
        
        - Considerations for choosing the right dataset for a specific application.

**5. Approaches and Methods**

- Object tracking methods involve detecting and localizing objects, then tracking them across frames.
    
- Methods are categorized into classical and deep learning approaches.
    
    - **5.1. Detection and Localization Methods:**
        
        - Classical approaches use techniques like background subtraction and optical flow.
        - Deep learning approaches use convolutional neural networks (CNNs).
    - **5.2. Tracking Methods:**
        
        - Tracking by detection involves detecting objects in each frame and then associating the detections.
        - Joint detection and tracking methods perform detection and tracking in a single framework.
    - **5.3. Recommendations for Approaches and Methods for Applications:**
        
        - Guidelines for choosing appropriate methods based on the application requirements.

**6. Applications**

- Object tracking is used in various fields.
    
    - **6.1. Medical:**
        
        - Tracking for surgical guidance and biomechanical assessment.
    - **6.2. Autonomous Vehicles:**
        
        - Tracking vehicles, pedestrians, and other road users.
    - **6.3. Surveillance:**
        
        - Monitoring areas for security and safety.
    - **6.4. Robotics:**
        
        - Enabling robots to perceive and interact with their environment.
    - **6.5. Agriculture:**
        
        - Tracking for tasks like crop monitoring and harvesting.
    - **6.6. Space and Defense:**
        
        - Tracking objects in space or for defense applications.

**7. Discussion**

- Discussion of the reviewed methods and datasets.
    
    - **7.1. Methods:**
        
        - Analysis of the strengths and limitations of different tracking methods.
    - **7.2. Datasets:**
        
        - Discussion of the characteristics and challenges of different datasets.

**8. Limitations and Future Work**

- Identifies limitations in current object tracking and suggests future research directions.
    
- Discusses challenges like real-time processing and handling dynamic environments.

**9. Conclusions**

- Summarizes the key findings of the review.
    
- Emphasizes the importance of object tracking in computer vision.

### D. Main methods & Explanation

**Detection and Localization Methods:**

- **Classical Approaches:**
    
    - These methods use image processing operations and algorithms.
        
    - Common techniques include background subtraction, optical flow, and template matching.
        
    - Classical methods are often tailored to specific applications and may involve empirically selected parameters.
        
- **Deep Learning Approaches:**
    
    - These methods use convolutional neural networks (CNNs) to detect and localize objects.
        
    - Deep learning models can achieve higher accuracy and can be trained end-to-end.
        
    - Common deep learning architectures include R-CNN, Faster R-CNN, and YOLO.
        

**Tracking Methods:**

- **Tracking by Detection:**
    
    - This approach involves detecting objects in each frame of a video and then associating the detections across frames to form tracks.
        
    - It separates the detection and tracking processes.
        
- **Joint Detection and Tracking:**
    
    - This approach performs detection and tracking simultaneously in a single framework.
        
    - It often uses end-to-end learning to predict object locations across frames.