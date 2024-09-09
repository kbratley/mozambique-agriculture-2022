# Mozambique Active Agricultural Extent Mapping (2022)

## Overview
This project maps active agricultural land extent in Mozambique for 2022 using Sentinel-2 Level-2A Surface Reflectance imagery. The analysis was conducted using a combination of the [DEA Sandbox](https://www.digitalearthafrica.org/) and [Google Earth Engine (GEE)](https://earthengine.google.com/) platforms. This repository provides an overview of the methodology, results, and access to the data used in this study.

## Data Access
The final [Mozambique’s Active Agriculture Extent Map (2022)](https://code.earthengine.google.com/aa4700f748e76095ae5fa4e15fa19b5d) is available on Google Earth Engine (GEE).

## Data Description

The mapping of Mozambique's active agricultural land in 2022 was conducted using the Digital Earth Africa (DEA) crop-type mapping workflow, an open-source process that leverages Sentinel-2 geomedian composites and machine learning techniques. This workflow was adapted for use within the DEA Sandbox and Google Earth Engine platforms.

### Data Preparation
The analysis used publicly available Sentinel-2 geomedian composites from Digital Earth Africa. These composites, which reduce spatial noise and highlight dominant spectral characteristics, included:

 - 1 annual composite for 2022
 - 4 quarterly composites: Jan-Mar, Apr-Jun, Jul-Sep, and Oct-Dec
 - Additionally, three Median Absolute Deviation (MAD) layers were calculated for each composite to capture variability:

 - Euclidean MAD (EMAD): Measures the distance of each pixel from the median in multi-dimensional space.
 - Spectral MAD (SMAD): Captures spectral variability.
 - Bray-Curtis MAD (BCMAD): Measures spatial arrangement and heterogeneity.
Six spectral indices, including NDVI, LAI, and Tasseled Cap transformations, were calculated to improve vegetation monitoring and land-cover differentiation.

### Land Cover Mapping
A modified version of The [DEA crop-type mapping workflow](https://github.com/digitalearthafrica/crop-type) was employed to map agricultural areas using a Random Forest classifier trained on data from 34,604 sites across Mozambique, with about 30% labeled as Agriculture and 70% as Other (non-agriculture). These sites were evenly distributed across provinces, with slightly lower densities in larger provinces and areas with uniform land cover.

The classifier produced a final map of Mozambique’s active agriculture, which showed that in 2022, 12% of the country’s land—approximately 90,680.57 km² ± 8,127.49 km²—was under cultivation. The majority of agricultural activity was concentrated in the provinces of Nampula, Zambezia, and Tete, correlating with higher population densities.

### Accuracy Assessment
A total of 1,200 reference sites were selected using simple random sampling to assess the accuracy of the map. Trained interpreters determine reference land cover labels for each unit in the sample by examining time series of Sentinel-2 and PlanetScope (Planet Team, 2017) data (2019-2022) using the [AREA2 toolbox](github.com/bullocke/area2). The final map achieved an overall accuracy of 96.9%, with specific accuracies for the Agriculture class at 89.32% (User) and 83.02% (Producer). 

## Citation
If you use this dataset, please cite as follows:
Bratley, K. (2022). Mozambique active agricultural land mapping. GitHub. (https://github.com/kbratley/mozambique-agriculture-2022)
