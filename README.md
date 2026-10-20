
# Cardiac MRI Segmentation Using CNN, Transformer, and Graph Neural Networks

## Project Overview

The research proposes a novel framework based on a fusion of CNN, Transformer, and GNN-based deep learning architectures for multiclass cardiac magnetic resonance imaging (MRI) segmentation.

The objective is to apply Convolutional Neural Networks (CNNs), Vision Transformers, and Graph Neural Network (GNN) hybrid architectures for identifying three important cardiac structures:

- Right Ventricle (RV)
- Myocardium
- Left Ventricle (LV)

Three architectures were evaluated across three cardiac MRI datasets using six segmentation performance metrics.

## Datasets

The following datasets were used:

1. **ACDC (Automated Cardiac Diagnosis Challenge)**
2. **M&Ms (Multi-Centre, Multi-Vendor and Multi-Disease Cardiac Segmentation)**
3. **CMR-MULTI**

Segmentation labels were standardized across the datasets:

| Label | Cardiac Structure |
|---|---|
| 0 | Background |
| 1 | Right Ventricle (RV) |
| 2 | Myocardium |
| 3 | Left Ventricle (LV) |

## Model Architectures

### 1. ResNet34 U-Net (CNN)

- ImageNet-pretrained ResNet34 encoder
- U-Net decoder for pixel-level segmentation
- Serves as the CNN baseline

### 2. Swin-Small UPerNet (Transformer)

- Pretrained Swin-Small Transformer backbone
- Hierarchical window-based self-attention
- UPerNet segmentation architecture

### 3. ResNet34 + GraphSAGE U-Net (CNN-GNN Hybrid)

- ImageNet-pretrained ResNet34 encoder
- GraphSAGE layers for learning spatial feature relationships
- U-Net decoder for segmentation mask reconstruction

## Data Preprocessing

The preprocessing pipeline included:

1. Loading cardiac MRI images and segmentation masks.
2. Resizing images and masks to 224 × 224 pixels.
3. Converting grayscale MRI images into three-channel inputs.
4. Normalizing input images.
5. Standardizing segmentation labels.
6. Applying data augmentation during training.
7. Maintaining patient-level or case-level separation between dataset splits.

## Training Configuration

The models were implemented using Python and PyTorch in Google Colab.

- **Batch size:** 8
- **Loss function:** Cross-Entropy + Multiclass Dice Loss
- **Optimizer:** AdamW
- **Learning-rate scheduler:** ReduceLROnPlateau
- **Model selection:** Best validation Dice score
- **Early stopping:** Used to limit unnecessary training

## Evaluation Metrics

Six metrics were used to evaluate segmentation performance:

- Dice Similarity Coefficient
- Intersection over Union (IoU)
- ROC-AUC
- Structural Similarity Index Measure (SSIM)
- Hausdorff Distance (HD)
- 95th-percentile Hausdorff Distance (HD95)

Metrics were evaluated for the RV, Myocardium, and LV, with macro-average results used for model comparison.

## Experimental Results

### Mean Dice Scores

| Dataset | ResNet34 U-Net | Swin-Small UPerNet | ResNet34 + GraphSAGE U-Net |
|---|---:|---:|---:|
| ACDC | 71.52% | 70.97% | **74.67%** |
| M&Ms | 81.63% | 83.48% | **83.67%** |
| CMR-MULTI | 84.47% | **85.14%** | 84.52% |

### Key Findings

- The CNN-GNN hybrid achieved the highest Dice score on ACDC (74.67%).
- The CNN-GNN hybrid also achieved the highest Dice score on M&Ms (83.67%).
- Swin-Small UPerNet achieved the highest Dice score on CMR-MULTI (85.14%).
- The relative performance of the architectures varied across datasets.

These results suggest that segmentation performance depends on the dataset and architectural approach.

## Project Files

```text
cardiac-mri-segmentation/
|
|-- cardiac_mri_segmentation.ipynb
|-- README.md
|-- cardiac_mri_research_paper.pdf
```

The Google Colab notebook contains the implementation, training, evaluation, and visualization code for the three architectures.

The research paper contains additional experimental details, performance tables, and segmentation visualizations.

## How to Run

1. Download or clone this GitHub repository.
2. Open `cardiac_mri_segmentation.ipynb` in Google Colab.
3. Enable GPU acceleration under Runtime > Change runtime type.
4. Install the dependencies specified in the notebook.
5. Configure the dataset paths in the notebook.
6. Execute the notebook cells in order.

**Note:** Dataset access and paths must be configured before running the experiments. GPU resources are recommended for model training.

## Technologies Used

- Python
- PyTorch
- Torchvision
- Hugging Face Transformers
- GraphSAGE
- NumPy
- Pandas
- Matplotlib
- Google Colab

## Research Paper

**Title:** Domain Adaptation with Graph-TransResNet for Medical Image Segmentation

The manuscript attached presents the methodology, experimental results, and comparison of CNN, Transformer, and CNN-GNN approaches across three cardiac MRI datasets.

## Project Status

Research and manuscript development are ongoing.

## Disclaimer

This project is intended for academic research and educational purposes. The segmentation models are not validated for clinical diagnosis or medical decision-making.
