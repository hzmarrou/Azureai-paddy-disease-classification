
## Introduction
In the realm of agriculture, early detection and treatment of plant diseases are crucial for maintaining the health of crops and ensuring food security. With the advent of artificial intelligence (AI), particularly Azure AI Custom Vision service, farmers and agronomists now have a powerful tool at their disposal to identify and manage plant diseases more efficiently than ever before.

### Development
Azure AI Custom Vision is a cognitive service that enables users to build custom image classifiers using machine learning. It is particularly well-suited for applications such as a plant disease classifier due to its robust feature set and ease of use.

####  Data collection
The first step in building a classifier model is to collect a dataset of plant images. These images should include a variety of plants, both healthy and diseased, under different conditions and stages of infection.

For this example we collected the images from Kaggle, you can download them [here](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset).

#### Data tagging
Once the dataset is collected, each image must be tagged with labels indicating whether the plant is healthy or specifying the type of disease present. This step is critical as it serves as the foundation for training the AI model.

The images from Kaggle are already tagged by folder, also there are images for training and validation.


## Example from Kaggle
##  Paddy Disease Detection and Classification

This project focuses on automating the identification of diseases in paddy crops using computer vision techniques. Paddy (Oryza sativa), a staple food worldwide, is predominantly cultivated in tropical climates, particularly in Asia. However, paddy cultivation is highly susceptible to diseases and pests, which can cause yield losses of up to 70%. Effective disease management requires expert supervision, but the limited availability of crop protection experts makes manual diagnosis both time-consuming and expensive.

To address this challenge, this project leverages a dataset of labeled paddy leaf images to develop an AI-driven disease classification model. By automating the disease detection process, we aim to provide an efficient, cost-effective solution for paddy farmers to safeguard their crops.



### Dataset Overview
The dataset contains a total of 13,876 labeled paddy leaf images divided into two parts:

Training Set: 10,407 images (75%), labeled across ten categories:
Nine disease types
Normal (healthy) leaf
Test Set: 3,469 images (25%) for model evaluation.
Metadata Included
Each image is accompanied by additional metadata to enhance model accuracy:

Paddy Variety: The type of paddy.
Age: The age of the paddy in days.

