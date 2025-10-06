# 🦈 Shark Predictive Mapping – Neutronics Team | NASA Space Apps Challenge 2025

## 🌍 Project Overview
This project, developed by the **Neutronics Team** for the **NASA Space Apps Challenge 2025**, aims to build a predictive model capable of identifying the most likely marine regions to contain **sharks**.  
The project combines **satellite data** from different missions (SWOT, PACE, and MODIS) and integrates them using a **mathematical probability formula**, visualized in an **interactive map** generated via Python and Google Colab.

The purpose is to demonstrate how open satellite data and machine learning-inspired modeling can support **marine ecosystem monitoring**, **biodiversity protection**, and the understanding of **predator behavior** through environmental correlations.

---

## 📡 1. Data Acquisition and Ecological Context

The base datasets used in this project were obtained from **NASA’s satellite missions**:
| Dataset | Mission | Variable | Description |
|----------|----------|-----------|-------------|
| `SWOT_WindWave.nc` | SWOT | SWH (Significant Wave Height) | Ocean surface height and wave amplitude |
| `PACE_OCI.clorofila_fitoplancton.nc` | PACE | Chlorophyll-a concentration | Indicator of phytoplankton abundance |
| `AQUA_MODIS_Temperature.nc` | MODIS (Aqua) | Sea Surface Temperature (SST) | Ocean temperature at the surface |
| `mapa_interativo_tubarao.html` | - | - | Interactive heat map generated in Python |

These datasets represent key ecological indicators that affect **shark distribution**, such as:
- **Temperature:** influences metabolic activity and migration routes.  
- **Phytoplankton (Chlorophyll-a):** indicates primary productivity and abundance of prey.  
- **Wave height:** relates to surface mixing and accessibility for hunting.

---

## ⚙️ 2. Electronic Tag Prototype (ESP32 Tracking System)

To connect the real-world observation of sharks to the computational model, a **hardware prototype** was designed using an **ESP32 microcontroller**, simulating a **biotelemetry tag**.

### 🔧 Hardware Components
| Component | Function |
|------------|-----------|
| **ESP32** | Main processing and communication module |
| **GPS Module (NEO-6M)** | Provides geolocation (latitude, longitude) |
| **Temperature Sensor (DS18B20)** | Measures water temperature |
| **Pressure Sensor (BMP280)** | Simulates depth level |
| **Micro SD Card Module** | Stores sensor and position data |
| **Battery + Waterproof Casing** | Provides energy and protection in aquatic environments |

The prototype collects and transmits the data periodically, simulating a real shark tag, and generates telemetry that mirrors the satellite data structures used in the Python model.

This creates a **direct bridge between field measurements and satellite-derived modeling**, forming the backbone for future real-time predictive systems.

---


## 🧮 3. Mathematical Probability Formula

To quantify the probability of shark presence, the project applied a **weighted normalization formula** that integrates the three environmental variables — **chlorophyll (Chl)**, **sea surface temperature (SST)**, and **significant wave height (SWH)**:

$$
I = \alpha \cdot \left(1 - \frac{|SST - SST_{opt}|}{\Delta SST}\right) + \beta \cdot \left(\frac{Chl}{max(Chl)}\right) + \gamma \cdot \left(1 - \frac{SWH}{max(SWH)}\right)
$$

**Where:**

| Symbol | Meaning | Description |
|:-------:|:---------|:-------------|
| **I** | Shark Probability Index | Normalized between 0 and 1 |
| **α, β, γ** | Variable Weights | (0.5, 0.3, 0.2) respectively |
| **SSTₒₚₜ** | Optimal Temperature | Based on ecological literature |
| **ΔSST** | Temperature Range | Used for normalization |
| **Chl** | Chlorophyll Concentration | Indicates plankton presence |
| **SWH** | Significant Wave Height | Represents sea surface turbulence |

This formula produces a **composite map** of potential shark presence, normalized between **0 (low likelihood)** and **1 (high likelihood)**.

---

## 💻 4. Code Operation and Processing Pipeline

The entire data processing pipeline was implemented in **Google Colab** using **Python** and scientific libraries such as:
`xarray`, `rasterio`, `folium`, and `numpy`.

### 🧠 Processing Steps

1. **Load** the NetCDF datasets (PACE, MODIS, and SWOT).  
2. **Resample** all datasets to a common 0.1° grid for spatial alignment.  
3. **Normalize** each dataset to a 0–1 scale.  
4. **Apply** the probability formula to combine variables into a unified index.  
5. **Save** the result as `.nc` (NetCDF) and `.tif` (GeoTIFF) files.  
6. **Generate** an interactive heat map with **Folium**, applying a **Turbo color scale** from blue (low) to red (high) probability.

---

## 🗺️ 5. Final Output

The resulting map — **`mapa_interativo_tubarao.html`** — displays:

- Each point representing an analyzed region.
- **Hover and click** interactions showing the probability intensity (0–1).
- **Zoom and navigation** controls for user exploration.

### Example of Visualization

| Intensity | Color | Meaning |
|:-----------|:------|:--------|
| 0.0 – 0.3 | 🟦 Blue | Very low probability |
| 0.3 – 0.6 | 🟨 Yellow | Moderate probability |
| 0.6 – 0.9 | 🟧 Orange | High probability |
| 0.9 – 1.0 | 🟥 Red | Very high probability (most likely shark zones) |

---

## 🚀 6. Environmental Importance and NASA Challenge Impact

This project demonstrates how **open satellite data** can be leveraged to:

- Predict the **presence of apex predators** like sharks.  
- Monitor **ecosystem health** and **marine biodiversity**.  
- Support **conservation policies** and **sustainable fishing** strategies.  

By integrating **field sensor data (ESP32 Tag)** with **global satellite datasets**, the **Neutronics Team** presents a **scalable model** addressing the **NASA Space Apps 2025 Challenge** on shark tracking and ocean monitoring.

The tool allows scientists and conservationists to **visualize, quantify, and predict** shark behavior patterns based on environmental factors.

---

## 📂 Repository Structure

| File Name                              | Description                                |
|----------------------------------------|--------------------------------------------|
| `PACE_OCI.clorofila_fitoplancton.nc`   | Chlorophyll data (PACE mission)            |
| `AQUA_MODIS_Temperature.nc`            | SST data (MODIS Aqua)                      |
| `SWOT_WindWave.nc`                     | Sea wave height data (SWOT mission)        |
| `mapa_interativo_tubarao.html`         | Final interactive probability map          |
| `preprocessing_and_mapping.ipynb`      | Full Google Colab code                     |
| `README_EN.md`                         | This document                              |

---

To reproduce or visualize the analysis locally, install the required packages:

```bash
pip install xarray rasterio folium numpy matplotlib netCDF4
```
---

## 🧠 Authors

**Neutronics Team**  
NASA Space Apps Challenge 2025  
Brazil
