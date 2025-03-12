# STA2453-Fish-Tether-Project
## Overview

This project aims to classify fish species—specifically lake trout and smallmouth bass—using hydroacoustic sonar data. Traditional fish identification methods require physical capture, which can be invasive and time-consuming. By leveraging machine learning and deep learning models, this project seeks to develop a non-invasive classification method based on sonar frequency responses.

## Project Background

Understanding fish populations is essential for ecological research and fisheries management. Each fish species has a unique acoustic signature that can be analyzed using sonar technology. By processing hydroacoustic data, we aim to distinguish between lake trout and smallmouth bass without relying on physical measurements.

## Methods

Data Preprocessing

* Removed incomplete records, particularly lake whitefish data due to missing frequency values.
* Excluded physical measurements like fish length and weight to focus on non-invasive classification.
* Retained frequency columns (F45–F260) representing target strength values in decibels.
* Imputed missing frequency values using species-specific means to maintain biological differences.
* Introduced a temporal feature, time_elapsed, to capture how acoustic signatures evolve over time.

Model Development

* Classical Machine Learning Models:
* Tested logistic regression, random forest, and XGBoost.
* Applied class weighting to address dataset imbalance.
* Tuned hyperparameters using GridSearchCV.

Deep Learning Model:

* Implemented a GRU-based recurrent neural network to capture temporal patterns.
* Sequences were padded to a maximum length of 17 pings.
* Used masking to handle variable sequence lengths.

