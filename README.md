# SharkPredictor_NASAHackton2025_Project
A global shark presence prediction and mapping system combining satellite data (MODIS, SWOT, and PACE) with an environmental probability mathematical model, implemented in Python using Google Colab and integrated with Google Earth Engine.

Project: Shark Occurrence Prediction – NASA Hackathon 2025

This project aims to generate global probability maps of shark occurrences using satellite data: chlorophyll (PACE), sea surface temperature (MODIS), and wave height (SWOT). The final index combines these variables into a mathematical formula that estimates the likelihood of shark presence, allowing identification of high-risk or conservation-interest areas.

The code processes the data and produces both static and interactive maps, highlighting regions with higher index values (0–1). The interactive map uses the Turbo color scale (blue → red) to indicate probability intensity.

This project provides a powerful visual tool for researchers, environmental agencies, and conservation planners, helping protect marine ecosystems and contributing to biodiversity studies and coastal safety.

Key outcomes:

Global probability maps of shark presence.

Combined index of chlorophyll, temperature, and wave height.

Interactive and exportable visualizations in HTML and PNG.

Robust methodology that can be updated with new satellite data.


| Cell | Content / Function | Variables / Objects | Detailed Explanation |
|------|-----------------|------------------|--------------------|
| 1 | Google Drive connection | `drive` | Mounts Google Drive in Colab to access data files. |
| 2 | Library installation | `!pip install ...` | Installs all necessary libraries: `xarray` and `rioxarray` for NetCDF, `matplotlib` and `cartopy` for static maps, `plotly` and `folium` for interactive visualizations. |
| 3 | File paths definition | `path_pace`, `path_modis`, `path_swot` | Stores the paths of PACE, MODIS, and SWOT files in Drive; used to open datasets. |
| 4 | Dataset loading and checking | `ds_pace`, `ds_modis`, `ds_swot`<br>Function `open_dataset_safe()` | Opens NetCDF files using `xarray` safely, checks if they exist, and prints basic summary of each dataset. |
| 5 | Preprocessing | `preprocess_data()`<br>`chlor_a_norm`, `sst_norm`, `swh_norm` | Removes NaNs, averages over temporal dimension if present, and normalizes values to 0–1 scale. |
| 6 | Data combination | `combined_index`<br>`weight_chl`, `weight_sst`, `weight_swh` | Creates a combined environmental index using a weighted average of normalized chlorophyll, SST, and wave height data. |
| 7 | Plotting with Cartopy | `plot_global_map()`<br>`lat2d_pace`, `lon2d_pace`, `lat2d_modis`, `lon2d_modis` | Function for global plotting in PlateCarree projection; adds land, coastlines, oceans, gridlines, and colorbar; used for PACE, MODIS, and combined index. |
| 8 | Interactive visualization with Plotly | `fig` | Displays the combined index on an interactive map with zoom, pan, and hover value reading. |
| 9 | Interactive map with Folium | `m`, `heat_data` | Generates a global interactive map with heat points showing index intensity; useful for geographic exploration. |

**Notes:**  
- `preprocess_data()` is reusable for any 2D or 3D dataset.  
- `combined_index` is an example of a weighted index; weights can be adjusted for analysis purposes.  
- Visualization types can be combined: Cartopy for high-quality static maps, Plotly for interactive plotting, and Folium for geographic exploration.

