# Cross-Modality Breast Lesion Segmentation from Oracle ROIs

Code associated with the study:

**A Cross-Modality Analysis of U-Net, Attention U-Net, and Swin-Tiny U-Net for Breast Lesion Segmentation from Oracle ROIs Across Imaging Modalities**

The repository contains modality-specific workflows for mammography, DCE-MRI, and breast ultrasound. The three modalities are evaluated independently rather than pooled into a single network.

## Experimental design

| Modality | Development data | Held-out evaluation |
|---|---|---|
| Mammography | CBIS-DDSM | INbreast |
| DCE-MRI | I-SPY1 / I-SPY2 / NACT within MAMA-MIA | Duke within MAMA-MIA |
| Ultrasound | BUS-BRA | BrEaST |

The primary benchmark evaluates U-Net, Attention U-Net, and Swin-Tiny-U-Net using random seeds 42, 123, and 2025. Checkpoint and threshold selection are based on development validation data.

## Repository structure

```text
notebooks/
├── mammography/
├── dce_mri/
├── ultrasound/
└── supplementary/
    ├── mammography_posthoc/
    └── figures/
checkpoints_manifest.csv
requirements.txt
```

## Main execution order

### Mammography
1. `notebooks/mammography/01_prepare_roi_crops.ipynb`
2. `notebooks/mammography/02_train_primary_models.ipynb`
3. `notebooks/mammography/03_patient_level_analysis.ipynb`

### DCE-MRI
1. `notebooks/dce_mri/01_download_and_prepare_dce.ipynb`
2. `notebooks/dce_mri/02_roi_crop_audit.ipynb`
3. `notebooks/dce_mri/03_train_primary_models.ipynb`
4. `notebooks/dce_mri/04_patient_level_evaluation.ipynb`
5. `notebooks/dce_mri/05_statistical_analysis.ipynb`

### Ultrasound
1. `notebooks/ultrasound/01_download_and_prepare.ipynb`
2. `notebooks/ultrasound/02_train_primary_models.ipynb`
3. `notebooks/ultrasound/03_external_evaluation.ipynb`

The supplementary mammography notebooks reproduce the post hoc analyses reported separately in the manuscript. The figure notebook regenerates the architecture and qualitative figures from prepared data and model artifacts.

## Data availability

Imaging datasets are not redistributed with the repository. Dataset access remains subject to the conditions of the original providers.

The experiments use reference-mask-derived contextual ROIs and therefore represent localization-conditioned segmentation rather than end-to-end lesion detection.

## Model checkpoints

The large checkpoint files are not stored in the Git repository. `checkpoints_manifest.csv` provides the model, modality, seed, selected epoch, file name, SHA-256 checksum, parameter count, and verification status for the 27 primary validation-selected checkpoints.

Checkpoint weights can be distributed through a separate archival release.

## Environment

Required Python packages are listed in `requirements.txt`. GPU acceleration is recommended for model training.
