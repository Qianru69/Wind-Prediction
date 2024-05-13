# Wind-Prediction

This repo consolidates the deliverables for team Breezy Brains' CS 663 Machine Learning Final Project: Wind Energy Prediction. The team is made up of [Qianru Wei](https://www.linkedin.com/in/qianru-wei/) and [Lawrence Ng](https://www.linkedin.com/in/lawrence-sl-ng/).

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

We performed EDA of the above 3 datasets. The code for this can be found in:
* ERA5 EDA - `/Data-Preprocessing/ERA5_EDA_BayArea.ipynb` and `/Data-Preprocessing/ERA5_EDA_Chicago.ipynb`
* Wind Turbine Location EDA - `/Data-Preprocessing/Wind-Turbine-EDA.ipynb`
* Wind Turbine Power Curve EDA - `/Data-Preprocessing/Wind-Turbine-Energy-EDA.ipynb`

In the ERA5 EDA, we found that the data for the Chicago and San Francisco Bay Area are complete with no missing values. The most important variables from the dataset were Eastward and Northward Wind at 10 and 100 meter height. We performed feature engineering on these variables to obtain the actual wind speed along with wind direction in sine and cosine form.

In the Wind Turbine Location EDA, we found that the dataset contains over 70,000 active and inactive turbines in the United States with 28 columns of data. We reduced the dataset to include only active turbines at Chicago and San Francisco Bay Area. While we found few null values, we did find missing values masquerading as fake numerical value `-9999` or strings `"missing"`. We imputed these missing values using a variety of techniques, including using figure from nearby turbines or turbines within the same wind farm.

In the Wind Turbine Power Curve EDA, we noted that while the 2 sources gave slight inconsistencies, these are the best and most reasonable data we can obtain. We imputed missing energy curve data from similar turbines by make, model, and power output. 

## CNN-LSTM model

We first experimented with CNN-LSTM model using a small set of data, and this work is included under `/LSTM_Work/LSTM_Starter_Code.ipynb`.

Once we confirmed that the general code works, we created 2 notebooks:

* SF Bay Area - `/LSTM_Work/LSTM_BayArea.ipynb`
* Chicago - `/LSTM_Work/LSTM_Chicago_all.ipynb`

We created, trained, validated, and tested the models within these notebooks. The resultant models can be found under `/LSTM_Work/model_CNN_LSTM_BayArea.pt` and `/LSTM_Work/model_CNN_LSTM_Chicago.pth`.

We also compared our prediction against Pyrecast (NBM) model's prediction for a single time point. This work can be found in `/LSTM_Work/LSTM_BayArea_Continuation (Pyrecast Comparison).ipynb`.

These notebooks contain some of the plots used in our Final Presentation slides.

**Note: Additional files in csv formats are in the `LSTM_Work` directory as we saved intermediate data while working off of Google Colab to make re-running notebooks less tedious. They can mostly be ignored but can be referenced from where they are generated and ingested in the actual notebooks.**

## Wind Speed -> Wind Energy Prediction

We then convert wind speed predictions into wind energy predictions. We perform this for the San Francisco Bay Area only as that is our main area of interest. This work can be found in `/LSTM_Work/LSTM_BayArea_Continuation (Energy_Output).ipynb`. 

**Note: Additional files in csv formats are in the `LSTM_Work` directory as we saved intermediate data while working off of Google Colab to make re-running notebooks less tedious. They can mostly be ignored but can be referenced from where they are generated and ingested in the actual notebooks.**

## Summary

Our machine learning model predicted wind speed on our test data with an MSE of **1.13**. For more details, please refer to the Final Presentation slides also included under `/Final Presentation.pdf`.

## Acknowledgements

We want to extend a heartfelt thank you to all the guidance and help from the following individuals throughout our project:

* Prof. David Guy Brizan 
* Prof. David Saah
* Prof. Fernanda Lopez Ornelas
* Aditya Kunatharaju
* Parisa Abbasi
* Shane Romsos

