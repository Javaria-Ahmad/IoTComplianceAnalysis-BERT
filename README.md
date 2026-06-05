# IoTPrivComp: A Measurement Study of Privacy Compliance in IoT Apps
## Research Background

Research Conducted: 2022

This repository contains the implementation details of IoTPrivComp. It is forked here from the original research GitHub account to be included here as part of my portfolio. 

First Author: Javaria Ahmad

Ph.D. in Computer Science (Data Science and Security)

## Motivation
- Policies are incomplete or inconsistent with the actual practices and difficult to comprehend
- The compliance gap between privacy policies and privacy practices in IoT apps is yet to be investigated 
- The data for IoT apps is more sensitive than mobile apps
- Off-the-shelf tools for IoT code and privacy policy analysis provide insufficient performance

## Research Questions
IoTPrivComp aims to answer the following questions.
- What does the landscape of IoT app privacy compliance looks like?
- Which privacy compliance gaps exist in IoT apps?
- Are there any patterns in IoT privacy compliance gaps?

## IoTPrivComp Components
- Data Collection 
   - Identified popular IoT platforms and IoT devices from each platform
   - Identified manufacturers for the apps and collected all free IoT apps from manufacturers
   - Added wearable devices that directly connect to smartphones using WiFi or Bluetooth
   - Downloaded the privacy policies of the apps
- Ontology Definition
  -  Fine-tuned a pre-trained transformer-based BERT model on IoT-specific corpus
  -  Trained a Tok2Vec relation extraction classifier
  -  Applied the fine-tuned BERT model and Tok2Vec classifier to extract entity and data objects and relationships automatically
- Data Flow Analysis
  - Code analysis to identify sources, sinks and data flows
  - SuSi-MNB-IoT: a machine learning approach to classify sinks
     - Support for Android 29
     - Customization for IoT devices/apps
     - Advanced machine learning approach: Multinomial Naive Bayesian
     - Support for exported components
  - Data flow analysis: categorize flows based on classes and sink methods
- Policy Analysis and Flow-to-policy Consistency Analysis
   - PoliCheck-BERT-IoT for policy analysis and compliance validation
   - Improved PoliCheck/PolicyLint for policy analysis
      - IoT-specific ontology
      - Adapting State-of-the-Art NLP Model: Replace CNN with BERT fine-tuned with IoT-specific corpus of privacy policies
  - PoliCheck-BERT-IoT identifies five types of disclosures in privacy policies:
     - Clear, Vague, Omitted, Incorrect, Contradictory
  - First-party flow: entity name matches app name/domain
  - Third-party flow: entity name does not match app name/domain 

## Performance Evaluation of IoTPrivComp and Analysis
- SuSi-MNB-IoT achieved an average precision and recall of 96% for sensitive sink identification
- PoliCheck-BERT-IoT achieved an 87.94% precision and an 88.09% recall for identifying data objects, and a 90.89% precision and a 91.05% recall for identifying entities
- 12% apps have missing privacy policies while 11.7% have non-English policies
- 14.6% of all apps that disclose sensitive data had missing or non-English policies
- For IoT apps, 173 (62.5%) first-party data flows and 258 (78.2%) third-party flows were inconsistent
- For wearable apps, 52 (62.7%) first-party data flows and 98 (77.8%) third-party flows were inconsistent
- Most of the inconsistency are omitted disclosures: the app collects or shares data without disclosing the practice in the policy 
- IoT apps: 2.9% clear disclosures, 30% vague disclosures, 74.5% omitted disclosures
- Wearables: 6.6% clear disclosures, 29.8% vague disclosures, 79.3% omitted disclosures

## Contributions
Our primary contributions are three-fold:
- We conduct a measurement study to identify the privacy gaps between the privacy practices and disclosures in 1,951 IoT apps, a first attempt at this scale
- We have developed our own tools or adopted SOTA tools: developed SuSi-MNB-IoT and PoliCheck-BERT-IoT
- We have examined 1,951 IoT apps from Google Play Store and analyzed the privacy disclosure gaps

## Tech Stack
Python   
Pandas   
spaCy   
Transformers (BERT)   
SQLite

## Technical Details and Execution Steps

**Version information:**

spaCy version    3.2.2                         

Platform         Windows-10

Python version   3.7.4  

**Need the following directories/files created:**

/ext/combined_tables

/ext/plaintext_policies (place all the policy text files here to be analyzed)

/ext/input/policySubsets/1.txt (copy names of all the text files present in the folder above to this file) 

/ext/output/policy (pickle files will be generated here as a result of running this application)

/ext/datasets/1.txt (copy the names of the pickle files to this file that were generated under the folder above)

/ext/output/analytics

/ext/output/db/

/ext/output/log_data

/ext/data/flows.csv (your file containing the results of app data analysis and these columns = ['package_name', 'app_name', 'version_name', 'version_code', 'data_type', 'dest_domain', 'dest_ip', 'arb_number', 'privacy_policy'])


**Run the files in the following order:**

PatternExtractionNotebook

ConsistencyAnalysisNotebook

RemoveSameSentenceContradictionsNotebook

DisclosureClassificationNotebook
