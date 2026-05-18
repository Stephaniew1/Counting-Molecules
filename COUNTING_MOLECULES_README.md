# Counting Molecules: Automated Analysis of STM Imaging Data

A computer vision pipeline that automates the counting and classification of molecule species from Scanning Tunnelling Microscopy (STM) images, reducing manual inspection effort by 40 to 50 percent.

## Overview

Researchers using STM imaging to study molecular species typically count and classify molecules by hand, a slow and subjective process that does not scale to large image sets. This project builds an end-to-end pipeline that ingests raw STM images, segments individual molecules, and classifies them by species using scikit-learn.

## Problem

Given a folder of STM images containing multiple molecule species, automatically:

1. Read and standardise the raw image files
2. Convert each image into a clean binary mask separating molecules from background
3. Detect and segment individual molecules
4. Count molecules per species across the dataset

## Approach

The pipeline is split across three notebooks, each handling one stage of the workflow:

### 1. Reading and standardising STM images
`ReadSTM_images project (3).ipynb` ingests raw STM image files, handles the instrument-specific format, and produces a standardised image array ready for downstream processing.

### 2. Binarisation
`all images binarization.ipynb` applies thresholding and noise reduction across the image set to produce binary masks separating molecules from background. Threshold selection is tuned empirically against a labelled subset.

### 3. Blob detection and counting
`blob detection .ipynb` applies blob detection algorithms to the binary masks to identify, segment, and count individual molecules. Detected blobs feed into a scikit-learn classifier to assign species labels.

## Results

- 40 to 50 percent reduction in manual inspection effort compared to hand-counting
- End-to-end pipeline reproducible across new image sets without retuning
- Output: per-image counts and species classifications, exportable for downstream analysis

## Tech stack

- **Language:** Python
- **Libraries:** scikit-learn, scikit-image, OpenCV, NumPy, matplotlib
- **Environment:** Jupyter Notebook

## Repository structure

```
Counting-Molecules/
├── ReadSTM_images project (3).ipynb     # Stage 1: image ingestion and standardisation
├── all images binarization.ipynb        # Stage 2: thresholding and binarisation
├── blob detection .ipynb                # Stage 3: blob detection and classification
└── README.md
```

## Run

The three notebooks are designed to run in sequence. Each stage's output feeds the next.

```bash
git clone https://github.com/Stephaniew1/Counting-Molecules.git
cd Counting-Molecules
pip install scikit-learn scikit-image opencv-python numpy matplotlib jupyter

# Run in order:
jupyter notebook "ReadSTM_images project (3).ipynb"
jupyter notebook "all images binarization.ipynb"
jupyter notebook "blob detection .ipynb"
```

## Context

This project was completed during my Data Science Vacation Research Scholar placement at the University of Adelaide, in collaboration with researchers using STM imaging to study molecular surface chemistry.

## Limitations and future work

- Threshold parameters are tuned for the specific STM instrument used and may need adjustment for other setups
- Overlapping molecules can be miscounted; a deep learning segmentation model, for example U-Net, would handle dense regions more robustly
- The classifier is trained on a small labelled subset and would benefit from a larger, more diverse training set

## License

This project is for academic and portfolio purposes. See repository for details.
