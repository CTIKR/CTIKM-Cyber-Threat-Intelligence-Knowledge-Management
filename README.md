# CTIKR

Implementation of the paper *CTIKR: Towards Automatic Knowledge Management from Cyber Threat Intelligence*.

## Introduction
CTIKR(Cyber Threat Intelligence Knowledge Representation) is a tool to building a general knowledge representation of the cyber threat knowledge in OSCTI (Open-Source Cyber
Threat Intelligence) articles. The key idea of CTIKR is to the knowledge of cyber threats can be represented by the structured information of the CTI sentences, which are the sentences that describe the Cyber attack tactics or the Cyber attack behaviors.

## Requirements
Python Version >= 3.8.0
Python Library:
numpy >= 1.23.4
scikit-learn >= 1.1.2
simpletransformers >= 0.63.9
hdbscan >= 0.8.28
torch >= 1.12.1
networkx >= 2.8.7
cdlib >= 0.2.6

## Usage
CTIKR contains three main components: 
1. Automatic extraction of cyber threat knowledge. CTIKR has a knowledge base of CTI sentences based on existing cyber threat knowledge bases two machine learning models to identify the sentences. Detailed instruction is shown in XXX. 
2. Construction of article clusters and knowledge graph based on extracted knowledge. Detailed instruction is shown in XXX.
3. Four security applications based knowledge discovery of the cyber threat knowledge threat knowledge.

## Appendix

## Acknowledgement

