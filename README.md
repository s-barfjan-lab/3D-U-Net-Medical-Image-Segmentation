# 3D-U-Net-Medical-Image-Segmentation
3D U-Net model for lung segmentation from CT scans using the LCTSC dataset with data augmentation, Dice loss, and volumetric medical image preprocessing.
# 3D U-Net Lung Segmentation on CT Scans

## Project Overview

This project implements a **3D U-Net deep learning model** for automatic lung segmentation from CT scans.

The system loads volumetric medical images in NIfTI format, applies preprocessing and augmentation, and trains a 3D convolutional neural network to predict lung masks.

The model is trained and evaluated using the **LCTSC lung CT segmentation dataset**.

This project demonstrates a complete pipeline for:

- Medical image loading
- Preprocessing and normalization
- 3D data augmentation
- U-Net architecture implementation
- Dice loss optimization
- Training with generators
- Evaluation and visualization


---

## Dataset

Dataset format:
data/data/lctsc/<patient_id>/
ct.nii.gz
lung.nii.gz


- ct.nii.gz → CT volume
- lung.nii.gz → segmentation mask

Total patients: 60

Images are resized to:
64 × 64 × 64 × 1


Each voxel is normalized using HU windowing.


---

## Preprocessing

Steps:

- Load NIfTI volumes with nibabel
- Apply HU windowing
- Normalize values to [0,1]
- Convert masks to binary
- Resize to fixed shape

Windowing function:
windower(data, wmin=-1000, wmax=300)



---

## Train / Test Split
90% training
10% testing


Data generators are used to avoid loading all augmented data into memory.


---

## Data Augmentation

3D augmentation applied during training:

- Random rotations
- Elastic deformation
- Batch generation with Sequence

Techniques based on:

- Simard elastic deformation
- Random 3D rotation
- On-the-fly augmentation

Generator:
LungAugSequence



---

## Model Architecture

Custom **3D U-Net** with:

- Conv3D layers
- Batch normalization
- Residual connections
- Dropout regularization
- Skip connections
- Transposed convolutions

Structure:
Down blocks
Bottleneck
Up blocks
Sigmoid output

Input shape:
(64,64,64,1)



---

## Loss Function

Dice Similarity Coefficient (DSC)

dice_loss = 1 − dice_coefficient

Used for medical segmentation because it measures overlap.


---

## Optimizer

Adam with cosine decay:
Adam + CosineDecayRestarts


Early stopping used to prevent overfitting.


---

## Training

Training settings:

- Epochs: 50
- Batch size: 2
- Early stopping enabled

Final validation Dice ≈ 0.91


---

## Results

The model successfully segments lungs from CT scans.

Outputs:

- Predicted mask
- Ground truth mask
- CT slice

Plots include:

- Prediction vs GT
- Dice over epochs


---

## Visualization

Examples show:
Prediction
Ground truth
CT image


And training curves:


Train Dice
Validation Dice



---

## Dependencies
tensorflow
keras
numpy
matplotlib
nibabel
scipy
sklearn


Example:


pip install tensorflow keras nibabel scipy matplotlib numpy



---

## Files
Unet-Lung-Segmentation.ipynb
data/
models/
plots/


---

## Author

Shima Abdollahi Barfjan
Medical Image Segmentation Project  
Deep Learning / Computer Vision / Biomedical AI
