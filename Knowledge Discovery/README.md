# Knowledge Representation

The second part of CTIKR is to represent knowledge through article clusters and triple graphs.

## Introduction
CTIKR uses the two output models from the knowledge extraction component on the training OSCTI training articles to identify the CTI sentences from articles. Based on these CTI sentences, CTIKR then clusters the training OSCTI articles based on the features of their CTI sentences and outputs article clusters as the first type of the knowledge representation. 

The 'Article Clustering Results Training Set.xlsx' contains the extracted feature vectors of the CTI sentences from training OSCTI articles. Each row in the excel file represents a OSCTI article, and the columns shows the features. These feature are: results of tactic sentences and behavior sentences, tactics statistics of tactics sentences and CTI Sentences, sentence statistics of all sentences and CTI Sentences, IOC Words statistics of All sentences and CTI sentences, reduced dimensional model inference result embedding and reduced dimensional CTI sentence embedding.

CTIKR also adapt NLP techniques to identify the relations between CTI sentences and constructs a knowledge graph as the second type of the knowledge representation.

## Usage
To apply the article clustering algorithm, open the **Build article cluster.ipynb**, and load the **Article Clustering Results Training Set.xlsx** which already has different feature values. Run the **Import the data** cell to load the **Article Clustering Results Training Set.xlsx** to generate a dataframe **df_train** contains all values. Then run the **Generate the feature vector and cluster the blogs in the training set** cell to summary one feature vector based on different values, and cluster the OSCTI training articles based on the feature vector. The returned result is the new version of dataframe **df_train_cluster** which has a new column **HDBSCAN Cluster** to show the cluster number of each article and a variable **HDBSCANCluster** which is the HDBSCAN model.

To evaluate the clustering result, run the **Calculation of silhouette coefficient for the training sett** cell to calculate the silhouette coefficient of the clustering result. The value of the silhouette coefficient ranges from -1 to 1, where 1 represents the best clustering, -1 represents the worst clustering.

Additionally, run the **Generate the 2D visualization of the training set** cell to visualize the clustering result based on reduced dimensional feature vectors. Each point represents an article, and the color of the point represents the cluster of the article. Our clustering result is shown in the following figure.

![image](https://i.imgur.com/O1X5nri.jpg)
