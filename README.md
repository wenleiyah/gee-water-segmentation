# Water Body Segmentation and SVM Classification in Google Earth Engine

## Abstract

This project implements an enhanced workflow for coarse-grained **water body segmentation** using **multispectral Sentinel-2 and Landsat-8 imagery** in **Google Earth Engine (GEE)**.
By integrating **Principal Component Analysis (PCA)** and **Gray-Level Co-occurrence Matrix (GLCM)** texture features into a **Support Vector Machine (SVM)** classifier, the method improves segmentation accuracy of water surfaces under varying atmospheric and hydrological conditions, such as heavy cloud interference or seasonal flooding.
The workflow is specifically optimized for low- to medium-resolution multispectral data, where spectral mixing and terrain complexity make fine-grained segmentation challenging.

---

This repository contains the scripts for water body segmentation and Support Vector Machine (SVM) classification in Google Earth Engine (GEE). The workflow integrates multispectral information from Sentinel-2 and Landsat-8 imagery to detect and classify water bodies under varying environmental and atmospheric conditions. The study leverages the rich spectral characteristics of optical sensors—particularly the visible, near-infrared (NIR), and short-wave infrared (SWIR) bands—to discriminate water from other surface materials.

By combining spectral, principal component, and texture features, the approach enhances classification accuracy, especially in complex terrains or scenes affected by cloud interference

## Data sources

**Sentinel-2 (10 m)** and **Landsat-8 (30 m)** provide complementary multispectral data across the visible, **near-infrared (NIR)**, and **short-wave infrared (SWIR)** ranges, allowing robust discrimination between water and non-water surfaces. PCA reduces spectral redundancy, and GLCM texture features derived from the first principal component (PC₁) capture spatial patterns that strengthen the SVM classification.

## Project layout

```
├── README.md
├── Delivery
│   └── Enhanced Water Body Extraction Using PCA-Enhanced SVM Classifiers.pdf
└── src
    ├── main.js            # Orchestrates the end-to-end processing workflow
    └── modules
        ├── CloudMask.js   # Sentinel-2 cloud masking utilities
        ├── GLCM.js        # Texture feature helpers built on GLCM statistics
        └── PCA.js         # Principal component analysis helpers
        └── DataQuery.js   # Utility functions from Earth Observation course for data querying & visualization
```

## Module overview

- **`src/main.js`**
  - Defines the study region and loads Sentinel-2 and Landsat-8 collections.
  - Computes NDWI-derived water masks, prepares training and validation samples.
  - Invokes the PCA and GLCM modules to build additional features and runs two SVM classification experiments.
- **`src/modules/CloudMask.js`** encapsulates the Sentinel-2 SCL-based cloud masking logic, including buffer operations to reduce edge artifacts.
- **`src/modules/PCA.js`** provides helpers for calculating principal components and preparing visualization layers.
- **`src/modules/GLCM.js`** derives texture metrics (entropy, variance, dissimilarity) from the principal component imagery using GLCM statistics.
- **`src/modules/DataQuery.js`** Utility functions provided by the Earth Observation course instructor for data querying and visualization in GEE, including temporal mosaicking, coverage estimation, and layer display.

## How to use the scripts

1. Sign in to the [Google Earth Engine Code Editor](https://code.earthengine.google.com/).
2. Create a new script in the **Scripts** panel and paste the contents of `src/main.js`.
3. For each helper module, create a new **Module** script, paste the corresponding file from `src/modules`, and make sure the imports in the main script point to the correct relative or published module paths in your GEE workspace.
4. Adjust the study area, temporal filters, or SVM parameters as needed, then run the script to visualize the map layers and review console outputs.

## Notes

- The workflow is designed for multispectral optical imagery.
- The code relies on the global `ee` object and must run inside the GEE environment.
- Default study areas and asset paths point to example resources; replace them with assets that exist in your account.
- Tune the SVM hyperparameters and sampling strategy to match the requirements of your project and the available training data.

## Related Report

A detailed explanation of the dataset, preprocessing, PCA-GLCM feature extraction, and SVM classification evaluation can be found in the project deliverable:

📄 **Delivery/Enhanced Water Body Extraction Using PCA-Enhanced SVM Classifiers.pdf**  
*(Wenlei Yang, 2025 — Politecnico di Milano, Earth Observation coursework report)*

### Acknowledgment

Some utility functions in `DataQuery.js` were provided as part of the Earth Observation course materials at Politecnico di Milano.