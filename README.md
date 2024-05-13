# Wind-Prediction

This repo consolidates the deliverables for team Breezy Brains' CS 663 Machine Learning Final Project: Wind Energy Prediction. The team is made up of Qianru Wei and Lawrence Ng.

In this README, we will lay out the general ideas and steps of our projects and how the contents of this repo corresponds to each of these parts of the project.

Some of the tools and libraries used include:
* [Google Colab](https://colab.research.google.com/)
* [Google Earth Engine](https://earthengine.google.com/) and related Python libraries 
* [sklearn](https://scikit-learn.org/stable/)
* [Pytorch](https://pytorch.org/)

**Note: We used Google Colab to develop and run the code in this project. File directories in this repo's notebooks do not correspond to their relative positions within the repo structure, but reflect the directory structure in our shared Google Drive folder for this project. There are also graphics from Google Earth Engine that do not show up properly once downloaded without re-running the code.**

## Scope of this project

In order to predict wind energy, we set out the following tasks:

1. We will use ML models to predict Wind Speed based on historical data.
2. We will benchmark our model predictions against Pyrecast(NBM) wind predictions.
3. We will convert wind speed prediction into energy production prediction based on the wind turbine locations and model-type power curves.

For visualization purposes, final results are presented in Google Earth Engine maps, but as mentioned, these do not show up properly.

## Datasets used in this project

### ERA5 
This dataset from the European Centre for Medium-Range Weather Forecasts (ECMWF) contains global hourly data on weather variable such as wind speed, temperature, and humidity from 1940 to present and can be obtained [via this link](https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels?tab=overview). The dataset is too large to download all at once, so we selected the weather variables that we believe will be most useful in prediction of wind speed, and limited the selection to 2 geographic area: San Francisco Bay Area (latitude: {36.0 - 40.0} longitude: {-124.0 - -120.0}) and Chicago area (latitude: {41.0 - 42.0} longitude: {-88.0 - -87.0}). The actual files related to this dataset are not uploaded to this repo as they are too large to upload. They exist within our Google Drive folder for this project.

### Wind Turbine Location
This dataset from USGS provides the locations of land-based and offshore wind turbines in the United States and can be obtained [via this link](https://eerscmap.usgs.gov/uswtdb/). This dataset is included as a zipped file in the repo under `/Data-Preprocessing/uswtdbSHP.zip`. An associated Excel file with a description of the columns/features within the dataset is also included under `/Data-Preprocessing/uswtdb_v6_1_20231128_codebook.xlsx`.

### Wind Turbine Power Curve
This dataset is manually scraped from the following 2 sources:
* [The Wind Power turbine database](https://www.thewindpower.net/turbines_manufacturers_en.php)
* [wind-turbine-models.com turbine database](https://en.wind-turbine-models.com/turbines)

We retrieved known power curve figures for wind turbine models located in the San Francisco Bay Area and Chicago region and added them to a Google Sheet, which we later saved to a CSV. This CSV is included under `/Data-Preprocessing/Wind Turbine Information Clean.csv`.

## EDA of datasets


## CNN-LSTM model

## Wind Speed -> Wind Energy Prediction

## Acknowledgements
