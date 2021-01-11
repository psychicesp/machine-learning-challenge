# Exo-Planet Classifier
This analysis uses exoplanet data from the Kepler space telescope, stored in **'exoplanet_data.csv'**

With little background on this data set, it seemingly is a series of metrics the Kepler space telescope transmits when it finds an object likely to be an exo-planet.  Presumably this data is then analyzed by NASA and determined if the object is 'CONFIRMED' as an exo-planet or was a 'FALSE POSITIVE' as denoted in the 'koi_disposition' column.  Objects not yet confirmed or denied are labelled 'CANDIDATES'.  

The eventual classifier created is an ensemble of  K Nearest Neighbors, Support Vector, and Random Forest classifiers. Initially a logistic regressor was used in lieu of KNN, but the accuracy of it was too similar to SVM, which was the exact accuracy of the ensemble classifier. This suggested that they were returning the exact same predictions.  With 2 of 3 classifiers always voting the same, this defeats the purpose of an ensemble method, so it was replaced with KNN.   The trained classifiers are stored as serialized .pickle files in **'pickle_jar'.**

In **'1_KNN.ipynb'** the data from **'exoplanet_data.csv'**
