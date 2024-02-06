# Revenue-predictor

# 1. Overview
This is a project that I have worked on with 6 other colleagues for the Exploratory Data Analysis course in my first year of Computer Engineering Masters. My role was to work on data preparation, data exploration (feature selection and preprocessing) and also I developed a Random Forest classifier in order to split the data into clusters. The aim of this project is to analyze company information from the lens of revenue prediction.

# 2. Methodology

## 2.1 Problem statement
Our team project focuses on utilizing the Veridion API to analyze companies and implement a
straightforward **revenue prediction system**. At the core of our approach is a systematic data processing
pipeline. 

The dataset consists of a number of company attributes, and we employ clustering algorithms in order to
group them on the basis of their estimated revenues. The clusters are used as labels for classification on the one hand, and regression for direct revenue prediction, on the other hand. Both the former and the latter
approach allow further insight into company characteristics.

## 2.2 Data & applied techniques
Our dataset of **~50,000** companies was derived using the Veridion API. Initially, a pool of ~500,000
companies was extracted. We employed a not-null filtering for certain attributes that might be relevant
for the company revenue, such as:

- no of employees
- no of headquarters
- business tags
- company type
- technologies
- country
- year founded
- insurances

We removed irrelevant features like: name, email, phone and social media links.

The dataset encompasses various attribute types, including:
- Numerical - integer, floats
- List of numericals - we retain the maximum dimension, with padding applied using zeros for the remaining values, ensuring data integrity.
- Text - we used label encoding where text possibility wasdiscrete, like the case of country code. For text of indefinite length, like company description, we employed a BERT-like transformer to encode the text, averaging all tokens’ encoding to obtain a whole sentence encoding.


Numerical values, excluding those encoded with the transformer, underwent normalization using min-max scaling,
confined within the range of 0 to 1.

# 3. Implementation
Beginning with data collection, we extract real-time and historical information from the Veridion API.
Subsequently, a carefully designed processing pipeline involves filtering and preprocessing to refine the data for meaningful analysis.

Recognizing the importance of revenue, we employ clustering techniques to categorize companies based on their
revenue profiles. This clustering process organizes companies into ranges, facilitating structured analysis and anomaly detection for companies with exceptionally high revenues.

Building on the clustered revenue data, our project integrates a classification system that efficiently assigns
companies to predefined revenue ranges. This classification step enhances the precision of subsequent regression analyses, allowing for nuanced predictions tailored to each range.

In the final phase, precise regression models are applied to each revenue range, providing detailed and
accurate revenue predictions. This report outlines our modest yet effective approach, emphasizing the systematic nature of our pipeline.







