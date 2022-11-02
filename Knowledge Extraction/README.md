# Knowledge Extraction

The first step of CTIKR is to train classification model and automatically obtain different types of CTI sentences from OSCTI articles using NLP model. We use the python library **simpletransformers** to perform model training and inference.

## Introduction
This file **CTI_sentences.xlsx** contains sentences from OSCTI articles for the purpose of training of the classification model and following evaluation. The 'Sentence' column contains the sentence text, the 'Tactics' column contains the sentence's Cyber attack tactic label, and the 'Behavior' column contains the sentence's Cyber attack behavior label.

We labeled every sentences of the 672 article from ATT&CK knowledge base, and got 8,408 sentences. Then, we use active learning with uncertainty sampling to label 9,012 sentences from 5,110 OSCTI articles.

In total, 17,420 sentences are labeled with the Cyber attack tactics. Among the 17,420 sentences, we further labeled 1,023 sentences describing attack behavior and 940 sentences not describing attack behavior as the negative samples.

## Requirements

simpletransformers >= 0.63.9

## Usage
The CTIKR already provide two trained model, you can use the following code to load the model and predict the CTI sentences. 

The active learning greatly improves the performance of tactic model. Our tactic model has average **88% precision** and **90% recall**, and our behavior model has average **83% precision** and **82% recall**. The following table shows tactic model performance on individual tactics before and after active learning.

![image](https://i.imgur.com/2B7wEg2.jpg)

To use the model, download the **'tactic model.zip'** or **'behavior model.zip'** file and unzip at the same folder. Open the jupyter notebook Knowledge Extraction Model Training.ipynb, modify the variable ** my_best_model_dir** to './model'. Then only run the **'Setup'** and **'Evaluation'** cell. The variable y_pred contains the list of inference results. 

For train own model, you should input the training data as the 'sentence.pkl' at the **'Setup'** cell, then run the **'Training'** cell. The model training and evaluation follow the k-fold cross validation. At each fold, the input format dataframe should be [[text1, label1], [text2，label2], ..., [textn，labeln]] with integer label . After running the 'Training' cell, the trained model will be saved at the 'clfmodel/k/best_model' folder.
