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

To quantify the probability of shark presence, the project applied a **weighted normalization formula** that integrates the three environmental variables (chlorophyll, SST, and SWH):

```math
I = α * (1 - |SST - SSTₒₚₜ| / ΔSST) + β * (Chl / max(Chl)) + γ * (1 - SWH / max(SWH))
Where:

𝐼
I: Shark probability index (0 to 1)

𝛼
,
𝛽
,
𝛾
α,β,γ: Weights for each variable (0.5, 0.3, 0.2 respectively)

𝑆
𝑆
𝑇
𝑜
𝑝
𝑡
SST 
opt
​
 : Optimal temperature for shark activity (based on ecological literature)

Δ
𝑆
𝑆
𝑇
ΔSST: Temperature range normalization

𝐶
ℎ
𝑙
Chl: Chlorophyll concentration

𝑆
𝑊
𝐻
SWH: Significant Wave Height

This formula produces a composite map of potential shark presence, normalized between 0 (low likelihood) and 1 (high likelihood).

💻 4. Code Operation and Processing Pipeline
The entire data processing pipeline was implemented in Google Colab using Python and scientific libraries such as:
xarray, rasterio, folium, and numpy.

🧠 Processing Steps
Load the NetCDF datasets (PACE, MODIS, and SWOT).

Resample all datasets to a common grid (0.1° resolution) to ensure spatial alignment.

Normalize each dataset to a 0–1 scale.

Apply the probability formula to combine the variables into a unified index.

Save the result as NetCDF (.nc) and GeoTIFF (.tif) files.

Generate an interactive heat map with folium, plotting each point with a color scale (Turbo) from blue (low) to red (high) probability.

🗺️ Final Output
The resulting map, mapa_interativo_tubarao.html, displays:

Each point representing a region analyzed by the model.

Hover and click functionality to view intensity values (0–1).

Zoom and navigation controls for user exploration.

🌐 5. Example Visualization
Below is a conceptual representation of how the probability intensity is visualized:

Intensity	Color	Meaning
0.0 – 0.3	🟦 Blue	Very low probability
0.3 – 0.6	🟨 Yellow	Moderate probability
0.6 – 0.9	🟧 Orange	High probability
0.9 – 1.0	🟥 Red	Very high probability (most likely shark zones)

🚀 6. Environmental Importance and NASA Challenge Impact
This project demonstrates how open satellite data can be used to:

Predict the presence of apex predators like sharks.

Monitor ecosystem health and marine biodiversity.

Support conservation decisions and sustainable fishing policies.

By integrating field-inspired sensor data (ESP32 Tag) with global satellite datasets, the Neutronics Team presents a scalable model that fulfills the NASA Space Apps 2025 challenge on shark tracking and ocean monitoring.

The tool allows both scientists and conservationists to visualize, quantify, and predict shark behavior patterns based on environmental drivers.

📂 Repository Structure
plaintext
Copiar código
/
├── PACE_OCI.clorofila_fitoplancton.nc      # Chlorophyll data from PACE mission
├── AQUA_MODIS_Temperature.nc               # SST data from MODIS Aqua
├── SWOT_WindWave.nc                        # Sea wave height data from SWOT
├── mapa_interativo_tubarao.html            # Final interactive probability map
├── preprocessing_and_mapping.ipynb         # Full Google Colab code
└── README_EN.md                            # This document
🧩 Dependencies
To reproduce or visualize the analysis locally:

bash
Copiar código
pip install xarray rasterio folium numpy matplotlib netCDF4
🧠 Authors
Neutronics Team
NASA Space Apps Challenge 2025
Brazil
