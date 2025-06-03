
### A. Paper
![[HarrisOriginalpaper.pdf]]

### B. Keywords

| **Keyword**                   | **Explanation**                                                                               |
| ----------------------------- | --------------------------------------------------------------------------------------------- |
| **Corner Detection**          | Identifying points in an image where intensity changes sharply in multiple directions.        |
| **Edge Detection**            | Locating boundaries between regions with significant intensity changes.                       |
| **Auto-correlation Function** | Measures local image variations to detect features like corners and edges.                    |
| **Moravec’s Corner Detector** | Early corner detector using discrete shifts to find high-intensity-change regions.            |
| **Harris Corner Detector**    | Improved method using eigenvalues of the auto-correlation matrix for robust corner detection. |
| **Eigenvalues (α, β)**        | Describe the shape of the auto-correlation function (flat, edge, or corner).                  |
| **Corner Response (R)**       | Scalar metric combining eigenvalues to classify corners: $R=det⁡(M)−k⋅tr(M)^2$                |
| **Non-Maximum Suppression**   | Retains local maxima in corner response to eliminate duplicate detections.                    |
| **Junction Completion**       | Connects edges and corners to form a coherent edge-vertex graph.                              |
### C. Summary of the Paper

The paper introduces the **Harris Corner Detector**, a robust method for detecting corners and edges in images. It addresses limitations of earlier techniques like Moravec’s detector by:

1. Using **continuous gradient approximations** (avoiding anisotropic responses).
2. Employing a **Gaussian window** for smoother, noise-resistant calculations.
3. Leveraging the **auto-correlation matrix (M)** and its eigenvalues to distinguish corners, edges, and flat regions.  
4. The detector’s **corner response function (R)** combines rotational invariance with efficient computation, enabling reliable feature extraction for 3D scene reconstruction and motion analysis.

### D. Main Methods Explained

1. **Moravec’s Corner Detector (Baseline)
	
	- An early corner detector that measures intensity changes in discrete directions but suffers from anisotropy and noise sensitivity.
	- **Principle**: Shifts a small window in discrete directions (e.g., 45° increments) and measures intensity changes (SSD).
	    
	- **Limitations**:
	    - Anisotropic (misses corners not aligned with shifts).
	    - Noisy due to binary rectangular windows.
	    - Poor edge discrimination (only uses minimum SSD).
	- **Example**: Fails on diagonal edges (Figure 4a).

2. **Harris Auto-correlation Detector
	
	- Improves Moravec’s method using continuous gradients and an auto-correlation matrix to robustly identify corners and edges.
		
	- **Improvements**:
	    - **Continuous Gradients**: Uses $I_x​, I_y​$ (Sobel/Prewitt filters) for all directions.
	    - **Gaussian Window**: Smooths noise and weights central pixels more.
	    - **Auto-correlation Matrix (M)**:
	        $M=[∑Ix2∑IxIy∑IxIy∑Iy2]$
		    
	    - **Eigenvalue Analysis** - Classifies regions as flat (small eigenvalues), edges (one large eigenvalue), or corners (both eigenvalues large) based on the auto-correlation matrix.
	        - **Flat**: $α≈β≈0$
	        - **Edge**: One eigenvalue $≫0$, the other $≈0$.
	        - **Corner**: Both eigenvalues large.

3. **Corner Response Function (R)
	
	- A scalar metric $R=det⁡(M)−k⋅tr(M)^2$ that quantifies corner strength (positive), edges (negative), or flat regions (near-zero).
	- To avoid explicit eigenvalue computation, Harris defines a corner response:
		
		$R = det⁡(M) − α * trace(M)^2 = λ_1*λ_2 − α*(λ1+λ2)^2$
		
	- **$det⁡ (M) = λ1 * λ2$: Measures corner strength (large for corners).
	- $trace(M)=λ1+λ2$​: Penalizes edges (avoids false positives).
	- $α$ : Empirical constant (typically 0.04–0.06).

4. **Response Interpretation**
	
	- *R>threshold*: Corner.
	- *R<0: Edge.
	- *∣R∣ small: Flat region.

- 5. **Edge-Corner Integration
	
	- Links detected edges to nearby corners to form a connected edge-vertex graph for structural scene analysis.
	- **Edge Thinning**: Retains edgels with local minima in gradient direction.
	- **Junction Completion**: Links edges to nearby corners for connectivity (Figure 7).

### E. Key Contributions

1. **Rotation Invariance**: Uses gradients and eigenvalues, unlike Moravec’s discrete shifts.
2. **Robustness**: Gaussian window reduces noise; auto-correlation matrix handles texture.
3. **Unified Framework**: Combines corner/edge detection for 3D scene analysis.