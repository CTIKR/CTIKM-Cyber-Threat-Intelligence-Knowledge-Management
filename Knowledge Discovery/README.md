# Knowledge Discovery



## Introduction


## Usage
For topic classification, open the **Topic Classification.ipynb**, and load the **Article Clustering Results Test Set.xlsx** which already has different feature values. Run the **Import the data** cell to load the **Article Clustering Results Test Set.xlsx** to generate a dataframe **df_test** contains all values. Then run the **Generate the feature vectors and cluster the blogs in the test set.** cell to summary one feature vector based on different values and find the most similar cluster in the training set based on the feature vector and **HDBSCANCluster**. The returned result is  list **testLabel ** that contains cluster of article in the test set.
