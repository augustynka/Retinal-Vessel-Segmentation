## Retinal-Vessel-Segmentation

This repository accompanies the report and provides a complete pipeline for automatically detecting blood vessels in fundus images of the retina.

**Key Components:**
- **Image Preprocessing & Masking**  
  - Load and decompress PPM-.gz files; convert to grayscale and enhance contrast (CLAHE).  
  - Automatically generate Field-of-View (FOV) masks and apply morphological cleaning.

- **Classical Vessel Detection (Frangi Filter)**  
  - Apply Frangi vesselness filter to highlight tubular structures.  
  - Threshold, post-process and mask results, then compute pixel-level metrics (accuracy, sensitivity, specificity, balanced score).

- **k-Nearest Neighbors Classifier**  
  - Extract handcrafted patch-based features (intensity variance, gradient magnitude, Hu moments).  
  - Balance classes via undersampling; tune decision threshold via ROC/Youden’s J.  
  - Real-time overlay visualizations of TP/FP/FN on sample images.

- **Random Forest Classifier**  
  - Replace K-NN with a balanced-class Random Forest (100 trees, class_weight=’balanced’).  
  - Similar feature extraction and thresholding workflow, with comparative performance gains.

- **Patch-Based CNN**
  - Define and train a small CNN on image patches (5×5) with dropout and early stopping.  
  - Evaluate patch-level segmentation and reconstruct full-image predictions.
  - Although a patch-based approach is not the most appropriate for full-image vessel segmentation, it was tested to evaluate feasibility and gain insights into patch-level performance.

- **U-Net Segmentation**  
  - Full-resolution U-Net architecture (256×256 input) with weighted binary cross-entropy to address class imbalance.  
  - Two-stage train/val/test split, skip connections, and advanced callbacks (EarlyStopping, ReduceLROnPlateau).  
  - Comprehensive evaluation and overlays, with discussion of challenges and future improvements.
