# Mozambique Active Agricultural Extent Mapping (2022)

---

## Overview
This project maps active agricultural land extent in Mozambique for 2022 using Sentinel-2 Level-2A Surface Reflectance imagery. The analysis was conducted using a combination of the [DEA Sandbox](https://www.digitalearthafrica.org/) and [Google Earth Engine (GEE)](https://earthengine.google.com/) platforms. This repository provides an overview of the methodology, results, and access to the data used in this study.

### Data Access
The final [Mozambique’s Active Agriculture Extent Map (2022)](https://code.earthengine.google.com/aa4700f748e76095ae5fa4e15fa19b5d) is available on Google Earth Engine (GEE).

### Data Description
The mapping was conducted using the Digital Earth Africa (DEA) [crop-type mapping workflow](https://github.com/digitalearthafrica/crop-type), which leverages Sentinel-2 geomedian composites and machine learning techniques. The workflow was adapted for the DEA Sandbox and GEE platforms.

#### Key Data Inputs:
**1. Sentinel-2 Geomedian Composites (from DEA):**
   - Annual Composite for 2022.
   - Quarterly Composites: Jan-Mar, Apr-Jun, Jul-Sep, and Oct-Dec.
**2. Median Absolute Deviation (MAD) Layers:**
   - Euclidean MAD (EMAD): Highlights pixel variability in multi-dimensional space.
   - Spectral MAD (SMAD): Captures spectral variability.
   - Bray-Curtis MAD (BCMAD): Captures spatial arrangement and heterogeneity.
**3. Spectral Indices:** NDVI, LAI, and Tasseled Cap transformations were included to improve vegetation monitoring and land-cover differentiation.

---

## Methodology Overview

### Training Data Collection (GEE)
- Training datasets were prepared using Google Earth Engine, with individual JavaScript scripts for each Mozambican province.
- These datasets were labeled with two classes: **Agriculture** and **Other**, based on 34,604 sites across the country.
- The `merge_trainingData` script combined provincial datasets into a single **national training dataset** for model training.

### Land Cover Classification (DEA)
- Python scripts accessed DEA datasets, processed imagery, and applied a **Random Forest classifier**.
- Classification was performed using the collected training data to map active agriculture for 2022.

### Accuracy Assessment and Area Estimation (GEE)
- The **AREA2 toolbox** in GEE was used to validate the map and estimate agricultural areas.
- Accuracy metrics, including **User’s and Producer’s accuracy**, were computed for the Agriculture class.

---

## Scripts Overview

### **1. Training Data Scripts**
- **Folder**: `1_training_data_GEE`
- **Purpose**: Collect training data for each province using GEE.
- **Scripts**:
  - Individual scripts for each Mozambican province (e.g., `Zambezia_Train`, `Maputo_Train`).
  - **`merge_trainingData`**: Combines provincial datasets into a national training dataset.
- **Outputs**: Labeled training data exported from GEE.

### **2. Classification Scripts**
- **Folder**: `2_land_cover_mapping_DEA`
- **Purpose**: Perform image classification using DEA datasets and Python.
- **Scripts**:
  - Sequential Python scripts within the `Moz_cropmask` folder:
    1. Extract and inspect training data.
    2. Train and evaluate a Random Forest model.
    3. Predict agricultural land cover using Sentinel-2 data.
    4. Combine image tiles into a seamless classification map.
    5. Compute zonal statistics for agricultural area estimation.
- **Outputs**: A classified map of Mozambique’s active agriculture in 2022 (GeoTIFF format) and zonal statistics summarizing agricultural area by region.

### **3. Accuracy Assessment Scripts**
- **Folder**: `3_accuracy_assessment_GEE`
- **Purpose**: Validate classification results and estimate areas using the [AREA2 toolbox](https://github.com/bullocke/area2) in GEE.
- **Scripts**:
  - Sequential scripts to:
    1. Generate random sampling points for accuracy assessment.
    2. Extract time-series data from Sentinel-2 imagery for sampled points.
    3. Assign reference labels to sampled points.
    4. Export labeled points for accuracy analysis.
    5. Combine all labeled points into a single feature collection.
    6. Perform stratified accuracy assessment and compute area estimates.
- **Outputs**: Accuracy report with metrics (e.g., overall accuracy, User’s and Producer’s accuracy) and area estimates for Mozambique’s agricultural land.

---

## Results Summary

### Land Cover Mapping
- Approximately **12% of Mozambique’s land (90,680.57 km² ± 8,127.49 km²)** was under cultivation in 2022.
- The provinces with the highest agricultural activity are **Nampula**, **Zambezia**, and **Tete**, correlating with high population densities.

### Accuracy Assessment
- **Overall Accuracy**: 96.9%.
- **Agriculture Class Accuracy**:
  - **User’s Accuracy**: 89.32%.
  - **Producer’s Accuracy**: 83.02%.

---

## How to Use This Repository

### Training Data Collection
1. Run the GEE JavaScript scripts in `1_training_data_GEE` to collect provincial training data.
2. Use the `merge_trainingData` script to combine datasets into a national dataset.

### Land Cover Classification
1. Use Python scripts in `2_land_cover_mapping_DEA` to classify Sentinel-2 imagery.
2. Ensure access to DEA datasets and install the required Python libraries.

### Accuracy Assessment
1. Run the GEE scripts in `3_accuracy_assessment_GEE` to validate the classified map output from the `2_land_cover_mapping_DEA` step and estimate areas using the AREA2 toolbox.

---

## Requirements

### Google Earth Engine (GEE)
- Required for Steps 1 and 3.
- Ensure you have a GEE account and access to the AREA2 toolbox.

### Python Environment
- Required for Step 2.
