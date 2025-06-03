
### A. Paper
![[OpticalFlow_JCEI2013.pdf]]

### B. Keywords & Explanation

|Keyword|Explanation|
|:--|:--|
|Optical Flow|The pattern of apparent motion of image objects between two consecutive frames caused by the movement of object or camera.|
|Lucas-Kanade (LK)|A local optical flow technique that assumes neighboring pixels have similar motion.|
|Horn-Schunck (HS)|A global optical flow technique that uses a smoothness term to regularize the flow field.|
|Motion Constraint|An equation that relates the image intensity changes to the optical flow.|
|Aperture Problem|The inability of an optical flow method to uniquely determine motion at each pixel.|
|Multi-Resolution|A technique that uses a pyramid of images at different resolutions to handle large displacements.|
|Warping|The process of transforming one image towards another using the estimated optical flow.|
|Non-Quadratic Penalizer|A function used to weight the influence of neighboring pixels in the LK method, reducing the impact of those that violate the coherence assumption.|
### C. Brief Summary

**I. INTRODUCTION**

- The paper revisits classical Lucas-Kanade (LK) and Horn-Schunck (HS) optical flow techniques.
    
- It aims to provide a baseline for other researchers on these two techniques.
    
- The formulations incorporate modern practices like multi-channel processing, multi-resolution with refinement, non-quadratic penalizers, and non-linear formulation of the brightness assumption.
    
- The paper evaluates the performance enhancement from each modern practice.
    
- It also seeks to renew the performance of LK and HS for fair comparison to state-of-the-art techniques.
    

**II. CONCEPTS OF THE OPTICAL FLOW**

- Differential methods for optical flow rely on assumptions like brightness constancy and temporal consistency.
    
- These assumptions lead to the motion constraint equation.
    
- The motion constraint is an ill-posed problem with one equation and two unknowns.
    
- This leads to the aperture problem, where only the velocity component in the direction of the spatial gradient can be measured.
    
- Additional constraints are needed to obtain a well-posed problem.
    
- Techniques use different assumptions, such as the neighbor concept, to estimate optical flow.
    
- Optical flow techniques were initially classified as local (LK) and global (HS), but modern approaches combine both.
    

**III. COLOUR VERSION OF THE LUCAS-KANADE**

- Local techniques like Lucas-Kanade use the spatial coherence assumption, which assumes neighboring pixels move coherently.
    
- The Lucas-Kanade method estimates optical flow by minimizing the sum of constraints over a neighborhood.
    
- This paper uses an extended and multi-channel version of LK, combining the three color channels.
    
- The size of the neighborhood is a key concern, as textureless regions can make the system singular.
    

**IV. COLOUR VERSION OF THE HORN-SCHUNCK**

- Global approaches like Horn-Schunck use a smoothness term to avoid singularities and propagate information across uniform regions.
    
- Horn-Schunck minimizes a quadratic error functional with a data term (motion constraint deviation) and a smoothness term (deviation from smoothness flow assumption).
    
- The paper reformulates Horn-Schunck with a multi-channel formulation.
    
- The smoothness term allows flow propagation in regions lacking gradient information but can blur the flow at motion boundaries.
    

**V. MODERN FORMULATIONS**

- First-order Taylor's expansion leads to a linear approximation of the motion constraint, valid only for small optical flow values.
    
- Large optical flow displacements cause aliasing and multimodal energy functionals.
    
- The optical flow constraint is changed to a nonlinear formulation, and a pyramidal structure handles large displacements.
    
- At each pyramid level, the current flow is used to warp the image at time (t+1) towards the image at time t.
    
- The temporal derivative is approximated by the first order of Taylor expansion to remove nonlinearity.
    
- Minimizing the energy functionals yields Euler-Lagrange equations.
    
- The optical flow is divided into the flow of the coarser level and the flow increment of the current level.
    
- The flow estimation starts at the coarsest level and refines the solution by warping the input image.
    
- The minimisation scheme follows the classical HS, with options for other schemes.
    
- For the LK method, weights can be set using a non-quadratic penalizer to identify and reduce the influence of neighbors that violate the coherence assumption.
    

**VI. EXPERIMENTS**

- The methods are implemented using similar schemes for reliable comparison.
    
- They are tested using test sequences and average angular error (AAE) and average end-point error (EPE) measurements.
    
- Modern implementations use a median filter and bicubic interpolation.
    
- A Gaussian convolution smoothing filter is applied to reduce noise.
    
- The paper evaluates single-color and multi-color versions of LK and HS, with variations in multi-resolution and iterative refinement.
    
- The impact of pyramidal structure, iterative refinement, and multi-color space is studied.
    

**A. LK Modern Formulation**

- The experiments show that a pyramidal structure with iterative refinement significantly increases the performance of LK.
    
- Multi-channel LK versions perform better than single-channel versions.
    
- Using a non-quadratic penalizer to identify and weight neighbors based on coherence further improves the results.
    

**B. HS Modern Formulation**

- The performance of HS versions, including original, multi-resolution, and multi-color, are analyzed.
    
- Similar to LK, a pyramidal formulation significantly improves HS performance.
    
- Multi-channel HS versions show performance gains compared to single-channel, though the gain is less than with LK.
    

**VII. CONCLUSION**

- The paper revisits and modernizes the Lucas-Kanade and Horn-Schunck optical flow methods.
    
- Modern practices like multi-resolution, iterative refinement, and multi-channel processing are applied.
    
- These practices improve the performance and enable a fairer comparison to state-of-the-art techniques.
    
- The multi-resolution strategy is identified as a key factor for handling large motion displacements.
    
- Multi-channel approaches and robust penal

### D. Methods & Explanations

- **Lucas-Kanade (LK):** This is described as a local technique.
    
    - It relies on the "spatial coherence assumption," which means that neighboring pixels are assumed to move together.
        
    - LK estimates optical flow by minimizing the sum of constraints over a small neighborhood of pixels.
        
    - The paper also details a multi-channel version of LK that combines information from all three color channels.
        
- **Horn-Schunck (HS):** This is described as a global approach.
    
    - Unlike local methods, HS uses a "smoothness term". This term helps to propagate information even in uniform regions and avoids singularities.
        
    - HS minimizes a quadratic error functional that includes a "data term" (measuring the deviation from the motion constraint equation) and a "smoothness term" (measuring the deviation from the smoothness flow assumption).
        
    - The paper also discusses a multi-channel version of the HS method.