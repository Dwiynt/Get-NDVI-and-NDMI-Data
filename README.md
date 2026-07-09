# Get-NDVI-and-NDMI-Data
# Sentinel-2 NDVI & NDMI Extractor using Google Earth Engine (Python & JS)

This repository contains scripts to automatically extract, process, and export **Normalized Difference Vegetation Index (NDVI)** and **Normalized Difference Moisture Index (NDMI)** from Sentinel-2 Harmonized Surface Reflectance data. The workflow is optimized to handle large areas of interest (AOIs)—such as the entire Java Island—without encountering cloud platform memory limits.

## 🚀 Features
* **Automated Cloud Masking:** Utilizes the Scene Classification Layer (SCL) from Sentinel-2 L2A to filter out clouds, cirrus, and shadows.
* **Memory-Optimized Processing:** Implements a direct cloud-backend batch export pipeline to prevent `User memory limit exceeded` errors during large-scale analysis.
* **Dual-Band Consolidated Export:** Calculates and stacks both NDVI and NDMI into a single, efficient multi-band GeoTIFF file exported straight to Google Drive.
* **Cross-Platform Support:** Available for both the native Google Earth Engine JavaScript Code Editor and a standalone Python script designed for Visual Studio Code (VS Code) or Google Colab.

---

## 🛠️ Methodology & Band Calculations

### 1. Cloud Masking (SCL-Based)
The script targets and filters out cloud shadows, low-probability clouds, medium/high probability clouds, and thin cirrus by masking pixels based on Sentinel-2's Scene Classification map:
$$\text{Mask} = \text{SCL}(3) \lor (\text{SCL}(7) < \text{SCL} \le \text{SCL}(10)) \equiv 0$$

### 2. NDVI (Normalized Difference Vegetation Index)
Used to quantify vegetation greenness and health using Red and Near-Infrared (NIR) bands:
$$\text{NDVI} = \frac{\text{B8 (NIR)} - \text{B4 (Red)}}{\text{B8 (NIR)} + \text{B4 (Red)}}$$

### 3. NDMI (Normalized Difference Moisture Index)
Used to monitor changes in plant water content using NIR and Short-Wave Infrared (SWIR) bands:
$$\text{NDMI} = \frac{\text{B8 (NIR)} - \text{B11 (SWIR1)}}{\text{B8 (NIR)} + \text{B11 (SWIR1)}}$$

---

## 📦 Prerequisites & Setup

### Python / VS Code Environment
Before running the Python script, ensure you have the required libraries installed in your local machine or virtual environment:

```bash
pip install earthengine-api geemap
