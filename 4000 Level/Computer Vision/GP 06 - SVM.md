### A. Report
![[GP_06_Team_YOLO_Report.pdf]]

### B. [Code](file:///d%3A/Projects/Learnings-CV/SVM/test.ipynb)

1. **Imports and Setup

	- The script begins by importing necessary Python libraries for:
	- Data handling (`pandas`, `numpy`)
	- Plotting (`matplotlib`)
	- Machine learning tasks (`scikit-learn` for preprocessing, model training, and evaluation)

2. **Loading and Cleaning Data
	
	- The breast cancer dataset is read from a CSV file. Non-informative columns such as `id` or unnamed index columns are removed to keep only meaningful features.
	
	- The target variable `diagnosis`, originally containing `'M'` for malignant and `'B'` for benign, is mapped to numerical values: `1` for malignant and `0` for benign. This is necessary for model training.
	
3. **Feature Separation and Preprocessing
	
	- The features (X) and labels (y) are separated. Any non-numeric values in the features are coerced into numbers. Missing values, if any, are replaced with the mean of the respective columns. This ensures the dataset is fully numeric and without nulls.
	
4. **Train-Test Split
	
	- The dataset is split into 80% training and 20% testing data. The `random_state=42` ensures reproducibility of results.
	
5. **Feature Scaling
	
	- SVM models are sensitive to the scale of features. So, `StandardScaler` is used to standardize the dataset by removing the mean and scaling to unit variance. The scaler is fitted on the training set and applied to both training and test sets.
	
6. **Model Training
	
	- An SVM classifier with a linear kernel is trained using the scaled training data. The regularization parameter `C=1.0` is used by default, balancing margin maximization and classification error.
	
7. **Predictions and Evaluation
	
	- Predictions are made on the test data. The model’s performance is evaluated using:
		- `classification_report` which shows precision, recall, F1-score, and support.
		- `accuracy` which measures the overall percentage of correct predictions.
		- `confusion_matrix` which shows the breakdown of true vs predicted labels.

### C. Results

- *Classification Report
	
	- **Benign (Class 0):**
	    - Precision: 0.97 → 97% of predicted benign cases were actually benign.
	    - Recall: 0.96 → 96% of actual benign cases were correctly predicted.
	    - F1-score: 0.96 → Harmonic mean of precision and recall.
	    - Support: 71 → Total actual benign cases in test set.
    
	- **Malignant (Class 1):**
	    - Precision: 0.93 → 93% of predicted malignant cases were actually malignant.
	    - Recall: 0.95 → 95% of actual malignant cases were correctly predicted.
	    - F1-score: 0.94 → Balance between precision and recall.
	    - Support: 43 → Total actual malignant cases in test set.
    
	- **Overall Accuracy:** 95.61%
	- **Macro Average F1:** 0.95 (averaged equally across classes)
	- **Weighted Average F1:** 0.96 (accounts for class imbalance)
	
	- These scores indicate the model is performing very well, with slightly better performance on benign cases.
	
- *Confusion Matrix Interpretation
	
	- From the image:
		- **True Positives (Benign correctly classified as Benign):** 68
		- **False Negatives (Benign misclassified as Malignant):** 3
		- **False Positives (Malignant misclassified as Benign):** 2
		- **True Positives (Malignant correctly classified as Malignant):** 41
	
- *This shows:
	
	- The model made only 5 classification errors out of 114 test cases.
	- It is more likely to incorrectly classify a benign case as malignant (3 times) than the reverse (2 times), which is preferable in medical settings to avoid missing dangerous cases.
	
- *Summary
	
	- The SVM model trained on the breast cancer dataset performs with high accuracy and strong precision/recall for both classes. The confusion matrix and classification report confirm that the model is reliable and effective in distinguishing between benign and malignant tumors, with very few misclassifications.

### D. Applications of SVM

1. **Handwritten Digit Recognition**  

   - SVMs classify digits (e.g., postal codes) by maximizing the margin between different digit classes, achieving high accuracy even with noisy data.  
   - *Example*: The paper tested SVMs on 16×16 pixel images, outperforming neural networks.  

2. **Medical Diagnosis (Disease Classification)**  

   - SVMs classify medical data (e.g., tumor vs. non-tumor cells) by learning optimal decision boundaries from patient records or imaging data.  
   - *Example*: Breast cancer detection using SVM on biopsy data.  

3. **Text and Sentiment Analysis**  

   - SVMs classify text into categories (e.g., spam vs. non-spam emails) or sentiment (positive/negative reviews) using high-dimensional feature spaces.  
   - *Example*: Twitter sentiment classification using word embeddings as input features.  

### E. Challenges & Improvements

| **Challenge**                     | **Improvement**                                                                 |
|-----------------------------------|--------------------------------------------------------------------------------|
| **High Computational Cost**       | Use efficient optimization (e.g., Sequential Minimal Optimization (SMO)) or approximate kernel methods (e.g., Random Fourier Features). |
| **Kernel Selection Difficulty**   | Cross-validation to compare polynomial, RBF, and linear kernels; automatic hyperparameter tuning (e.g., grid search). |
| **Sensitivity to Imbalanced Data**| Apply class weighting or resampling techniques (e.g., SMOTE for minority classes). |
| **Memory Issues with Large Datasets** | Use chunking (as mentioned in the paper) or online SVM variants (e.g., LASVM). |
| **Interpretability of Nonlinear SVMs** | Use SHAP/LIME for explainability or prefer linear SVMs when interpretability is critical. |

### F. Exam Questions with Answers

1. **Why does maximizing the margin improve generalization in SVMs?**  

   - *Answer*: A larger margin reduces overfitting by minimizing the VC-dimension, leading to better performance on unseen data.  
   - *Example*: In digit recognition, a wider margin ensures robustness to slight variations in handwriting.  

2. **What is the role of supporting patterns in SVM training?**  

   - *Answer*: Supporting patterns (support vectors) are the closest data points to the decision boundary; they define the optimal hyperplane.  
   - *Example*: In Figure 1 of the paper, only circled points influence the final classifier.  

3. **How does the kernel trick allow SVMs to handle nonlinear classification?**  

   - *Answer*: Kernels implicitly map data to higher dimensions where linear separation is possible (e.g., RBF kernel creates infinite-dimensional spaces).  
   - *Example*: A quadratic kernel $(x \cdot x' + 1)^2$ separates XOR-like data.  

4. **What is the impact of outliers on SVM, and how can it be mitigated?**  

   - *Answer*: Outliers can distort the margin; slack variables (soft-margin SVM) or outlier removal (via large $\alpha_k)$ mitigate their effect.  
   - *Example*: Figure 2 shows how MSE ignores outliers, while SVM flags them for review.  

5. **Compare the dual and primal formulations of SVM. When is each preferred?**  

   - *Answer*: The primal (direct) form solves for ${w}$, while the dual form uses $\alpha_k)$. Dual is preferred for nonlinear kernels and high-dimensional $\varphi$-space (e.g., polynomial classifiers).  
   - *Example*: For $K(\mathbf{x}, \mathbf{x}') = (\mathbf{x} \cdot \mathbf{x}')^3$, the dual avoids computing $varphi(\mathbf{x})$ explicitly.  