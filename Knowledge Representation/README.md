# Knowledge Representation

The second part of CTIKR is to represent knowledge through article clusters and triple graphs.

## Introduction
CTIKR uses the two output models from the knowledge extraction component on the training OSCTI training articles to identify the CTI sentences from articles. Based on these CTI sentences, CTIKR then clusters the training OSCTI articles based on the features of their CTI sentences and outputs article clusters as the first type of the knowledge representation. 

The 'Article Clustering Results Training Set.xlsx' contains the 52,354 articles from the OSCTI training set and their corresponding feature vectors. Each row in the excel file represents a OSCTI article, and the columns shows the features. These feature are: results of tactic sentences and behavior sentences, tactics statistics of tactics sentences and CTI Sentences, sentence statistics of all sentences and CTI Sentences, IOC Words statistics of All sentences and CTI sentences, reduced dimensional model inference result embedding and reduced dimensional CTI sentence embedding. The 52,354 articles are clustered into 18 groups with meaningful topics as follows:

| Group | Topic                                                                                                                                 |
|------:|---------------------------------------------------------------------------------------------------------------------------------------|
|     0 | Attacker claims excessive privileges for malicious code, reads data and connect to attacker's server.                                 |
|     1 | Attacker scans other systems in the local network and spreads malicious code.                                                         |
|     2 | Attacker hide themselves and evade security systems to achieve persistence in target system.                                          |
|     3 | Attacker compromises target systems such as running ransomware, performing bitcoin mining or DDOS attacks.                            |
|     4 | Attacker enter the target system without being noticed.                                                                               |
|     5 | Malicious code connects to a server on Interent and send some data to it.                                                             |
|     6 | Malicious code connects to attacker's server and send some very sensitive data such as passwords, photos or IP address.               |
|     7 | Attacker only enters the target system without performing other attacks.                                                              |
|     8 | Attacker enters the target system and connects to attacker's server to download and run additional malware.                           |
|     9 | Attacker uses a exploit to execute arbitrary code.                                                                                    |
|    10 | Malicious code downloads additional malicious programs and command from server and steals local data without uploading to the server. |
|    11 | Attacker directly executes the code and connects to the server.                                                                       |
|    12 | Malicious code connects to the attacker's server and downloads other malicious code without executing it.                             |
|    13 | Normal software execution and data reading behavior.                                                                                  |
|    14 | Malicious code executes undetected, connects to attacker's server and steals data.                                                    |
|    15 | Malicious code executes undetected.                                                                                                   |
|    16 | Malicious code executes undetected, steals data without connection to attacker's server.                                              |
|    17 | The attacker performs the attack through multiple steps and eventually steals the data.                                               |
|    18 | The attacker is already in the system and the deployed malicious code steals the data.                                                |

CTIKR also adapt NLP techniques to identify the relations between CTI sentences and constructs a knowledge graph as the second type of the knowledge representation.

## Usage
To apply the article clustering algorithm, open the **Build article cluster.ipynb**, and load the **Article Clustering Results Training Set.xlsx** which already has different feature values. Run the **Import the data** cell to load the **Article Clustering Results Training Set.xlsx** to generate a dataframe **df_train** contains all values. Then run the **Generate the feature vector and cluster the articles in the training set** cell to summary one feature vector based on different values, and cluster the OSCTI training articles based on the feature vector. The returned result is the new version of dataframe **df_train_cluster** which has a new column **HDBSCAN Cluster** to show the cluster number of each article and a variable **HDBSCANCluster** which is the HDBSCAN model.

To evaluate the clustering result, run the **Calculation of silhouette coefficient for the training sett** cell to calculate the silhouette coefficient of the clustering result. The value of the silhouette coefficient ranges from -1 to 1, where 1 represents the best clustering, -1 represents the worst clustering.

Additionally, run the **Generate the 2D visualization of the training set** cell to visualize the clustering result based on reduced dimensional feature vectors. Each point represents an article, and the color of the point represents the cluster of the article. Our clustering result is shown in the following figure.

![image](https://i.imgur.com/z8fkI6j.jpg)
