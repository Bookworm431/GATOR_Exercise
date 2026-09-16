# GATOR_Exercise
GATOR Lab exercise by Amelia Keefe

# UCF Campus NDVI Time-Series Analysis

## Overview
This project is a programmatic, cloud-native spatial analysis of the University of Central Florida (UCF) campus. It tracks the Normalized Difference Vegetation Index (NDVI) throughout the year 2023 to monitor vegetation health. This was completed as part of a UF GATOR Lab exercise to transition from traditional desktop GIS workflows to modern, cloud-based geoprocessing.

## Methodology
Instead of downloading gigabytes of raw `.tif` files, this project uses a "lazy loading" cloud-native approach:
1. **Data Discovery:** Queried the Element 84 Earth Search STAC API for Sentinel-2 L2A satellite imagery with less than 20% cloud cover.
2. **Lazy Loading:** Utilized `stackstac` to build a virtual data cube of the Red and Near-Infrared (NIR) bands bounded exactly to the UCF campus coordinates, avoiding unnecessary data downloads.
3. **Processing:** Calculated the NDVI for each pixel using the formula `(NIR - Red) / (NIR + Red)`. Filtered out spatial artifacts and `NaN` values (divide-by-zero errors from masked edges) before calculating the spatial mean for each date.
4. **Execution & Visualization:** Used `dask` via `.compute()` to execute the processing graph and `matplotlib` to plot the resulting 2023 time-series.

## Technologies Used
* **Python** (`pystac-client`, `stackstac`, `xarray`, `dask`, `matplotlib`)
* **STAC API** (Element 84 Earth Search)
* **Cloud-Native Geoprocessing**

## How to Run Locally
To run this notebook on your own machine, clone the repository and install the required dependencies:

```bash
# Clone the repository
git clone [https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git](https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git)

# Navigate to the directory
cd YOUR-REPO-NAME

# Install the required Python libraries
pip install -r requirements.txt
