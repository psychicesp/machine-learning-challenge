# Exo-Planet Classifier
This analysis uses exoplanet data from the Kepler space telescope, stored in **'exoplanet_data.csv'**

## The Dataset
With little background on this data set, it seemingly is a series of metrics the Kepler space telescope transmits when it finds an object likely to be an exo-planet.  Presumably this data is then analyzed by NASA and determined if the object is 'CONFIRMED' as an exo-planet or was a 'FALSE POSITIVE' as denoted in the 'koi_disposition' column.  Objects not yet confirmed or denied are labelled 'CANDIDATE'.  

## Pre-Processing
In **'1_KNN.ipynb'** the data from **'exoplanet_data.csv'** is read, entirely null columns and rows containing null values were dropped.  Rows with a 'koi_disposition' of **'CANDIDATE'** are separated out into **'pickle_jar/unknown_df.pickle'** for later classification. 

An initial 80/20 train_test_split is made and this split saved as **'pickle_jar/ensemble_split.pickle'** (as the ensemble training will not need hyperparameter tuning.) The training set was split again for a final split of 60/20/20 for Training/Tuning/Testing. MinMaxer was set for the data and the minmaxed split data was saved as **pickle_jar/split_data.pickle** and the scaler saved as **'pickle_jar/minmax_scaler.pickle'**

## Analysis
The eventual classifier created is an ensemble of  K Nearest Neighbors, Support Vector, and Random Forest classifiers. Initially a logistic regressor was used in lieu of KNN, but the accuracy of it was too similar to SVM, which was the exact accuracy of the ensemble classifier. This suggested that they were returning the exact same predictions.  With 2 of 3 classifiers always voting the same, this defeats the purpose of an ensemble method, so it was replaced with KNN. Each model was trained, tuned and tested with the same 60/20/20 split using the same random state, except for the ensemble which was fit with the training and tuning set combined. The trained classifiers are stored as serialized .pickle files in **'pickle_jar'.**

Each individual classifier was >98% accurate with the ensemble method(**'pickle_jar/combined_model.pickle'**) performing marginally better than its constituent parts.

## Predictions

The combined model was used to predict the koi_dispositions of unknown_df.  These were labelled either as 'Positive' or 'Negative' in **predicted.csv** in a new column called **'koi_disposition_prediction'**