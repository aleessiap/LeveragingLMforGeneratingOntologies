## Motivation

Ontologies have demonstrated their efficacy as potent solutions for representing domain knowledge, integrating data from diverse sources, and facilitating a wide range of semantic applications. In the scholarly domain, ontologies enable efficient study and exploration of the global research scene, structured extraction of information from scientific articles, classification of publications, and identification of research communities.
Creating a high-quality ontology requires the analysis of several experts. These experts must have in-depth knowledge of the field and be able to describe the concepts and their relationships. 

Currently, this process is usually done manually, requiring a lot of time and workforce and often resulting in outdated and coarse-grained representations. Consequently, researchers have been developing automated or semi-automated methods to create these taxonomies.


This repository contains the code and the data used in the paper: "Leveraging Language Models for Generating Ontologies of Research Topics". This work investigates the application of transformer-based language models to generate research topic ontologies.
In particular, it focuses on classifying the relationship between two research topics: t<sub>A</sub> and t<sub>B</sub>.
We defined four possible relationships:
 - ***supertopic***: t<sub>A</sub> is an ancestor of t<sub>B</sub>. In the datasets, it is represented by the number 0;
 - ***subtopic***: t<sub>A</sub> is a descendant of t<sub>B</sub>, represented by the number 1;
 - ***same_as***: t<sub>A</sub> and t<sub>B</sub> identify the same topic, represented by the number 2;
 - ***other***: t<sub>A</sub> and t<sub>B</sub> are linked by different relationships from the above, represented by the number 3.



## Folders

This repository is organised as follows:

### datasets
This folder contains the dataset used in the experiments described in the paper. It includes two other folders:
- LM_dataset
- feature-based dataset

  #### LM_dataset
  This folder contains the dataset used to train and test SciBERT.
  The dataset is composed of four columns:
  - _topics_:
  	it represents the couple of topics we want to analyse: _t<sub>A</sub>; t<sub>B</sub>_.  
  - _subject_:
  	it represents the first topic: t<sub>A</sub>. 
  - _object_:
  	it represents the second topic: t<sub>B</sub>.
  - _label_:
    it represents the relationship between the topics using the numerical representation (0 - _supertopic_, 1 - _subtopic_, 2 - _same_as_, 3 - _other_).
  
  The model does not use the columns _subject_ and _object_; they are represented just for clarity. 
  
  #### feature-based dataset
  This folder contains the dataset used to train and test the Random Forest Classifier and the Gradient Boosting Classifier.
  The dataset is composed of six columns:
  - _topics_:
  	it represents the couple of topics we want to analyse: _t<sub>A</sub>; t<sub>B</sub>_.  
  - _sub_occ_:
  	it represents the number of times the first topic t<sub>A</sub> appears in the abstracts of the papers in AIDA KG (in the paper is occA).
  - _obj_occ_:
  	it represents the number of times the second topic t<sub>B</sub> appears in the abstracts of the papers in AIDA KG (in the paper is occB).
  - _sub_in_occ_:
  	it represents the number of times both the first topic t<sub>A</sub> and the second topic t<sub>B</sub> simultaneously appear in abstracts of the papers in AIDA KG (in the paper is cooccurenceAB).
  - _subsumption_: 
  	it indicates the degree of overlap between the co-occurring topics. 
  - _label_:
  	it represents the relationship between the topics using the numerical representation (0 - _supertopic_, 1 - _subtopic_, 2 - _same_as_, 3 - _other_).
  
  The model does not use the column _topics_, it is represented just for clarity. 
  

### code
This folder contains the two scripts used for the experiments. It includes two other scripts:
- LM finetuning
- feature-based method

    #### LM finetuning
    This script contains the code for the finetuning and the testing of the model (SciBERT).
    
    #### feature-based method
    This script contains the code for training and testing the two machine learning models (Random Forest and Gradient Boosting). 

