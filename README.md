# CTIKM

## Introduction
CTIKM (Cyber Threat Intelligence Knowledge Management) is an innovative tool designed to efficiently manage and utilize the vast amount of knowledge derived from Open-Source Cyber Threat Intelligence (OSCTI) articles. With the fast-paced development of the Internet infrastructure and the increasing cyber threats that target organizations, knowledge of these threats is aggressively collected and shared through OSCTI. However, the information provided by traditional blacklists is limited and the manual effort required to extract knowledge from CTI articles is not scalable. 

By leveraging advanced NLP model and a handcrafted high-quality Cyber threat dataset from active learning, CTIKM effectively and automatically summarizes two key types of information from OSCTI articles: Entity-Relationship Summary and CTI Article Summary. For any given articles, CTIKM extracts the techniques and behaviors of cyber threats described in the article, reveals the relationships among security-related entities and their behaviors across this article and ohter OSCTI articles and further provides knowledge graph about the specific entity.

## Overview
CTIKM contains three main components. The overview figure is shown below.

![image](https://i.imgur.com/ctPhnKu.png)

1. [Knowledge Extraction](https://github.com/CTIKR/CTIKM/tree/main/Knowledge%20Extraction): CTIKM builds a high-quality dataset based on active learning and two high-performance text analysis models based on RoBERTa model, and extracts relevant cyber threat knowledge from OSCTI articles. The extracted knowledge is represented as CTI sentences with cyber attack tactic and cyber attack behavior labels.

2. [Knowledge Representation](https://github.com/CTIKR/CTIKM/tree/main/Knowledge%20Representation): CTIKM clusters OSCTI articles based on their CTI sentences, and constructs a knowledge graph using the clusters whose topics are valuable to security analysts.

3. [Knowledge Discovery](https://github.com/CTIKR/CTIKM/tree/main/Knowledge%20Discovery): CTIKM searches the knowledge graph to produce entity-relationship summaries, and leverages the CTI sentence information in the clusters to generate CTI article summaries.

## Tool Requirements
Python Version >= 3.8.0

Python Library:

numpy >= 1.23.4

scikit-learn >= 1.1.2

simpletransformers >= 0.63.9

hdbscan >= 0.8.28

torch >= 1.12.1

networkx >= 2.8.7

cdlib >= 0.2.6
