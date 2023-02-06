# Knowledge Representation

## Workflow
1. Remove the articles that were involved in the **Knowledge Extraction** dataset and divide the remaining articles into 70% test set and 30% training set.
2. Based on the **Knowledge Extraction** models, obtain the tactical label and behavioral label information of the articles in the training set. Create the **Article Clustering Results Training Set.xlsx** file by statistical analysis.
3. Use the **Article Clusters.ipynb** file to unsupervised cluster the articles in the training set into different groups.
4. Manually inspecting different article groups, summarizing their topics and accuracy of same topic in group in that table **Topics And Accuracy Of Article Clusters**.
5. Use **Knowledge Graph Building.ipynb** to extract entities and their relationship from selective articles as triples, and save them as pkl file [**cluster_extracts_high_value.pkl**](https://huggingface.co/CTIKR/CTIKM_Cyber_Threat_Intelligence_Knowledge_Management/blob/main/cluster_extracts_high_value.pkl) for further analysis.


## Introduction
CTIKM uses the two output models from the knowledge extraction component on the training OSCTI training articles to identify the CTI sentences from articles. Based on these CTI sentences, CTIKM then clusters the training OSCTI articles based on the features of their CTI sentences and outputs article clusters as the first type of the knowledge representation. 

From the 52,354 training OSCTI articles, CTIKM models identified 8,456 articles that contain CTI sentences. We split them into 6,764 training articles and 1,692 testing articles. The training articles are used to train the article clustering model. The testing articles are used to evaluate the clustering and application of article topic classification. The 'Article Clustering Results Training Set.xlsx' contains these 6,764 articles and their corresponding feature vectors. Each row in the excel file represents a OSCTI article, and the columns shows their features. These feature are: results of tactic sentences and behavior sentences, tactics statistics of tactics sentences and CTI Sentences, sentence statistics of all sentences and CTI Sentences, IOC Words statistics of All sentences and CTI sentences, reduced dimensional model inference result embedding and reduced dimensional CTI sentence embedding. The 52,354 articles are clustered into 18 groups with meaningful topics as follows:

<p align="center">
  <b>Topics And Accuracy Of Article Clusters</b>
</p>

| Group | Topic                                                                                                                                 | Rate of Same Topic |
|-------|---------------------------------------------------------------------------------------------------------------------------------------|--------------------|
| 0     | Attacker claims excessive privileges for malicious code, reads data and connect to attacker's server.                                 | 80.00%             |
| 1     | Attacker scans other systems in the local network and spreads malicious code.                                                         | 85.00%             |
| 2     | Attacker hide themselves and evade security systems to achieve persistence in target system.                                          | 85.00%             |
| 3     | Attacker compromises target systems such as running ransomware, performing bitcoin mining or DDOS attacks.                            | 70.00%             |
| 4     | Attacker enter the target system without being noticed.                                                                               | 100.00%            |
| 5     | Malicious code connects to a server on Interent and send some data to it.                                                             | 85.00%             |
| 6     | Malicious code connects to attacker's server and send some very sensitive data such as passwords, photos or IP address.               | 80.00%             |
| 7     | Attacker only enters the target system without performing other attacks.                                                              | 85.00%             |
| 8     | Attacker enters the target system and connects to attacker's server to download and run additional malware.                           | 85.00%             |
| 9     | Attacker uses a exploit to execute arbitrary code.                                                                                    | 70.00%             |
| 10    | Malicious code downloads additional malicious programs and command from server and steals local data without uploading to the server. | 70.00%             |
| 11    | Attacker directly executes the code and connects to the server.                                                                       | 75.00%             |
| 12    | Malicious code connects to the attacker's server and downloads other malicious code without executing it.                             | 55.00%             |
| 13    | Normal software execution and data reading behavior.                                                                                  | 66.70%             |
| 14    | Malicious code executes undetected, connects to attacker's server and steals data.                                                    | 65.00%             |
| 15    | Malicious code executes undetected.                                                                                                   | 57.10%             |
| 16    | Malicious code executes undetected, steals data without connection to attacker's server.                                              | 50.00%             |
| 17    | The attacker performs the attack through multiple steps and eventually steals the data.                                               | 13.30%             |
| 18    | The attacker is already in the system and the deployed malicious code steals the data.                                                | 45.00%             |

CTIKM also adapt NLP techniques to identify the relations between CTI sentences and constructs a knowledge graph as the second type of the knowledge representation. We extract triples from the the texts in group 1, 2, 4, 6, 7, 8, 11 and 14. The triples are further filtered using the confidence from the behavior model and NER model. The remaining triples are used to build a knowledge graph.  

## Introduction 
To apply the article clustering algorithm, open the **Build article cluster.ipynb**, and load the **Article Clustering Results Training Set.xlsx** which already has different feature values. Run the **Import the data** cell to load the **Article Clustering Results Training Set.xlsx** to generate a dataframe **df_train** contains all values. Then run the **Generate the feature vector and cluster the articles in the training set** cell to summary one feature vector based on different values, and cluster the OSCTI training articles based on the feature vector. The returned result is the new version of dataframe **df_train_cluster** which has a new column **HDBSCAN Cluster** to show the cluster number of each article and a variable **HDBSCANCluster** which is the HDBSCAN model.

To evaluate the clustering result, run the **Calculation of silhouette coefficient for the training sett** cell to calculate the silhouette coefficient of the clustering result. The value of the silhouette coefficient ranges from -1 to 1, where 1 represents the best clustering, -1 represents the worst clustering.

Our article clusters has following silhouette coefficient: 

| Group | Silhouette Coefficient |
|-------|------------------------|
| 0     | 0.254                  |
| 1     | 0.267                  |
| 2     | 0.103                  |
| 3     | 0.163                  |
| 4     | 0.167                  |
| 5     | 0.335                  |
| 6     | 0.242                  |
| 7     | 0.354                  |
| 8     | 0.171                  |
| 9     | 0.358                  |
| 10    | 0.101                  |
| 11    | 0.206                  |
| 12    | 0.334                  |
| 13    | 0.159                  |
| 14    | 0.126                  |
| 15    | 0.356                  |
| 16    | 0.242                  |
| 17    | 0.172                  |
| 18    | 0.095                  |

Additionally, run the **Generate the 2D visualization of the training set** cell to visualize the clustering result based on reduced dimensional feature vectors. Each point represents an article, and the color of the point represents the cluster of the article. Our clustering result is shown in the following figure.

![image](https://i.imgur.com/z8fkI6j.jpg)


To generate the knowledge graph, run each cell in **Knowledge Graph Building.ipynb** to extract triples and perform the related post-processing methods.

