# Landslide Susceptibility Analysis in Central Vietnam based on Statistical Index and Random Forest
The repository contains data and Jupyter Notebooks to perform a landslide susceptibility analysis in the catchment area of the Vu Gia and Thu Bon river systems in Central Vietnam. On the one hand, a Statistical Index approach in combination with a Weighting Factor is used, oriented towards [Meinhardt et al. (2015)](https://doi.org/10.1016/j.envsoft.2023.105759), and on the other hand, a machine learning approach (Random Forest) is utilized for comparison.

## Structure
- original data: `data`
- processing scripts: `proc`
- created files: `created`
    - aligned rasters: `aligned_rasters`
    - landslide susceptibility predictions: `predictions`
- required Python packages: `requirements.txt`

## Original Data (`data`)
- data provided and used by [Meinhardt et al. (2015)](https://doi.org/10.1016/j.envsoft.2023.105759)
- includes DEM, lithology, soil, landcover, precipitation, roads, distance to waterbodies, landslides inventory, viewshed
- for more information and license see data description and  [Meinhardt et al. (2015)](https://doi.org/10.1016/j.envsoft.2023.105759)

## Processing (`proc`)
Run Jupyter Notebooks in following order!

### `pre_processing.ipynb`
- **TODO**: change working directory to `/local/path/to/403_landslide_susceptibility_analysis/` at top of file
- Ordinary Kriging to create precipitation raster
- alignment and clipping of all input rasters to the DEM raster
- results stored in `aligned_rasters`

### `statistical_index.ipynb`
- **TODO**: change working directory to `/local/path/to/403_landslide_susceptibility_analysis/` at top of file
- calculation of Topographic Wetness Index (TWI)
- categorizing input rasters
- save categorized raster as `.pkl` file in `created` directory
- plot landslide distribution in categorized rasters
- calculate Statistical Index within viewshed
- calculate Weighting Factor for each input variable
- calculate landslide susceptibility for the whole study area
    - saved in `predictions` directory as `SI_landslide_susceptibility_map.tif`
- classify created landslide susceptibility within whole study area
    - saved in `predictions` directory as `SI_landslide_susceptibility_map_classified.tif`

### `random_forest.ipynb`
- **TODO**: change working directory to `/local/path/to/403_landslide_susceptibility_analysis/` at top of file
- prepare test and training data
- determine best feature combination (combination of input variables)
- encode categorized data for correct treatment by Random Forest
- initialize Random Forest model with best feature combination
- hyperparameter tuning
- determine the permutation feature importance
- predict landslide susceptibility within the whole viewshed
    - saved in `predictions` directory as `RF_landslide_susceptibility_map_viewshed.tif`
- predict landslide susceptibility for whole study area
    - saved in `predictions` directory as `RF_landslide_susceptibility_map.tif`

### `model_comparison.ipynb`
- **TODO**: change working directory to `/local/path/to/403_landslide_susceptibility_analysis/` at top of file
- load and prepare landslide susceptibility predictions
- calculate ROC-AUC and PR-AUC for Statistical Index and Random Forest model predictions
- investigate True Skill Statistics (TSS), precision and recall behaviour for different thresholds

## Created Files (`created`)
All GeoTIFFs with "(calculated in GIS)" were derived from the original data using GIS. Slope and aspect were created using the DEM and their respective ArgGIS Pro tools. Distance to roads was calculated using Euclidean Distance and `merge_road_tracks.shp`.
- aspect (calculated in GIS): `aspect.tif`
- DEM: `dem.tif`
- landcover: `landcover.tif`
- landslides: `landslides.tif`
- lithology: `litho.tif`
- distance to roads (calculated in GIS): `road_distance.tif`
- slope (calculated in GIS): `slope.tif`
- soil types: `soil.tif`
- viewshed: `view.tif`
- water distance: `water_distance.tif`
- dictionary (saved as pickle file) containing categorized input rasters created/stacked in `statistical_index.ipynb`: `categorized_rasters.pkl`

### `aligned_rasters`
Contains `pre_processing.tif` results and three rasters pre-processed in ArgGIS Pro.
- aspect (calculated in GIS): `aspect.tif`
- Euclidean distance to roads (calculated in GIS): `EucDist_roads_reclass.tif`
- landcover: `landcover.tif`
- landslides: `landslides.tif`
- lithology: `litho.tif`
- precipitation: `precipitation.tif`
- slope (calculated in GIS): `slope_gis.tif`
- soil: `soil.tif`
- viewshed: `view.tif`
- distance to waterbodies: `water.tif`

### `predictions`
- `SI_landslide_susceptibility_map.tif`: Statistical Index based landslide susceptibility map for whole study area
- `SI_landslide_susceptibility_map_classified.tif`: Statistical Index based classified landslide susceptibility map for whole study area
- `RF_landslide_susceptibility_map_viewshed.tif`: Random Forest based landslide susceptibility map for whole viewshed
- `RF_landslide_susceptibility_map.tif`: Random Forest based landslide susceptibility map for whole study area
- `RF_landslide_susceptibility_map_classified.tif`: Classified Random Forest based landslide susceptibility map for whole study area
