# Mozambique Active Agricultural Land Mapping (2022)

## Overview
This project maps active agricultural land in Mozambique for the year 2022 using Sentinel-2 Level-2A Surface Reflectance imagery. The analysis was conducted using a combination of the DEA Sandbox and Google Earth Engine (GEE) platforms. This repository provides an overview of the methodology, results, and access to the data used in this study.

## Data Access
The data for Mozambique’s active agriculture map is available on Google Earth Engine (GEE). You can access the data by following these steps:

1. Go to [Google Earth Engine](https://earthengine.google.com/).

## Methods

The mapping was carried out using Digital Earth Africa’s (DEA) crop-type mapping workflow, which combines Sentinel-2 geomedian composites with machine learning techniques. The workflow was adapted and applied on the DEA Sandbox and GEE platforms.

### 2.1 Data Preparation
Five Sentinel-2 geomedian composites were used to reduce spatial noise and emphasize dominant spectral features:

1 annual composite (2022)
4 quarterly composites (Jan-Mar, Apr-Jun, Jul-Sep, Oct-Dec)

Additionally, three Median Absolute Deviation (MAD) layers were calculated for each composite:
- **Euclidean MAD (EMAD)**: Measures the distance of each pixel from the median in multi-dimensional space.
- **Spectral MAD (SMAD)**: Captures spectral variability.
- **Bray-Curtis MAD (BCMAD)**: Measures spatial arrangement and heterogeneity.

We also calculated six spectral indices, such as NDVI, LAI, and Tasseled Cap transformations, to better monitor vegetation and differentiate land-cover types.

### 2.2 Land Cover Mapping
We used a modified version of the [DEA crop-type mapping workflow](https://github.com/digitalearthafrica/crop-type) to map agricultural areas in Mozambique by employing a Random Forest machine learning classifier. Training data was collected using Sentinel-2 imagery, with 34,604 sites across Mozambique labeled as Agriculture or Other. After iterative training and refinement, we produced a final map of 2022 agricultural areas.

### 2.3 Accuracy Assessment
A total of 1,200 reference sites were selected using simple random sampling to assess the accuracy of the map. The final map achieved an overall accuracy of 96.9%, with specific accuracies for the Agriculture class at 89.32% (User) and 83.02% (Producer). The total mapped area of agriculture was estimated at **90,680.57 km²** ± 8,127.49 km².

## Results

### 3.1 Training Data Collection
The training dataset contains 34,604 sites, approximately 30% of which were labeled as Agriculture, and 70% as Other (non-agriculture). The training data is distributed across all provinces, with slightly lower densities in larger provinces and regions with uniform land cover.

### 3.2 Mozambique 2022 Active Agriculture Mapping Results
Active agriculture covered **12%** of Mozambique’s land in 2022, or **90,680.57 km²**. Most agricultural areas were located in the provinces of Nampula, Zambezia, and Tete, which also have the highest population densities. This suggests a correlation between population distribution and agricultural activity in the country.

### 3.3 Accuracy Assessment and Area Estimation
The accuracy of the agricultural map was evaluated using the reference dataset. The overall accuracy was 96.9%, with area estimates and their 95% confidence intervals for both Agriculture and Other land cover classes provided below:

| Class        | Area Estimate (km²) | 95% Confidence Interval (km²) | User Accuracy | Producer Accuracy |
|--------------|---------------------|------------------------------|---------------|-------------------|
| Agriculture  | 90,680.57            | 8,127.49                     | 89.32%        | 83.02%            |
| Other        | 696,309.07           | 8,127.49                     | 97.81%        | 98.71%            |

Overall, the high accuracy values indicate that the final map is reliable for land use planning and agricultural monitoring.

## Citation
If you use this dataset, please cite as follows:
Bratley, K. (2022). Mozambique active agricultural land mapping. GitHub. (https://github.com/kbratley/mozambique-agriculture-2022)
