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

## 3.1 The whole process
Beginning with data collection, we extract real-time and historical information from the Veridion API.
Subsequently, a carefully designed processing pipeline involves filtering and preprocessing to refine the data for meaningful analysis.

Recognizing the importance of revenue, we employ clustering techniques to categorize companies based on their
revenue profiles. This clustering process organizes companies into ranges, facilitating structured analysis and anomaly detection for companies with exceptionally high revenues.

Building on the clustered revenue data, our project integrates a classification system that efficiently assigns
companies to predefined revenue ranges. This classification step enhances the precision of subsequent regression analyses, allowing for nuanced predictions tailored to each range.

In the final phase, precise regression models are applied to each revenue range, providing detailed and
accurate revenue predictions. This report outlines our modest yet effective approach, emphasizing the systematic nature of our pipeline.

The pipeline can be viewed [here](https://github.com/NacuAndrei/Revenue-predictor/blob/master/Pipeline%20%26%20Statistics/ProjectPipeline.png).

## 3.2 My part - Random Forest classifier

After the dataset was split into 2, respectively 4 clusters by KNN, the target for my Random Forest algorithm was to predict those newly assigned clusters.

For data preparation, I decided to drop the outliers - the data that did not belong to any cluster (2-4k examples out of 50k). Some features were irrelevant for the dataset, columns such as "long_description" or "business_tags" were dropped. Other features consisted in short lists that were a result of encodation. I kept those values by taking the mean, keeping the first value only, or calculating the mean by exluding null values. The method that I applied depended on the content of those lists.

After analyzing the feature importance, those labels that I decided to keep turned out to be taken into consideration by the model. You can view some plots and further information about my part in the [complete documentation](https://github.com/NacuAndrei/Revenue-predictor/blob/master/FullDocumentation.pdf).

# 4. Statistics

Most important observations:
- Most companies are from the US and Europe;
- California, Texas, New York and Florida account for a large number of companies;
- There are some companies which have a huge revenue compared to the majority of companies in the dataset;
- Most companies are recently founded (last 50 years);
- There are a lot of companies with less than 10 employees;
- Coordinates are very important for revenue prediction;
- As a conclusion, dataset is unbalanced.

For plots and more data analysis, you can view the [complete documentation](https://github.com/NacuAndrei/Revenue-predictor/blob/master/FullDocumentation.pdf).

# 5. Results

## 5.1 Whole results

Clustering results:

| Clustering Model | Silhouette Score |
| -- | -- |
| K-means two labels | 0.618 | 
| K-means four kabels | 0.590|
| DBSCAN two labels | 0.194 |
| DBSCAN four labels | 0.111 |

Classification results:

| Classification model | Macro F1 score | Precision class 1 | Recall class 1 | Precision class 2 | Recall class 2 |
|--|--|--|--|--|--|
| Random Forest | 0.66 | 0.73 | 0.34 | 0.78 | 0.95 |
| SVM | 0.56 | 0.35 | 0.44 | 0.75 | 0.68 |
| XGBoost | 0.66 | 0.56 | 0.47 | 0.80 | 0.68 |
| KNN | 0.57 | 0.39 | 0.36 | 0.75 | 0.77 |
| Ridge Classifier | 0.55 | 0.35 | 0.5 | 0.76 | 0.62 |
| CNB | 0.53 | 0.33 | 0.44 | 0.74 | 0.64 |
| MLP | 0.64 | 0.51 | 0.43 | 0.78 | 0.83 |

For complete results, plots and results analysis, see the [complete documentation](https://github.com/NacuAndrei/Revenue-predictor/blob/master/FullDocumentation.pdf).

## 5.2 My results from Random Forest classifier

I used RandomForestClassifier with 100 estimators from sklearn.ensemble. The results consist in a classification report (accuracy, precision, recall, f1 score) and a confusion matrix.

- For 2-label classification:

<tr><td>

| Label | Precision | Recall | F1 score |  
|-------|-----------|--------|----------|  
| 1.0 | 0.73 | 0.34 | 0.46 |                
| 2.0 | 0.78 | 0.95 | 0.86 | 
  
| Accuracy | Macro F1 score |
|-------|-----------|
| 0.77 | 0.66 |   

![Conf matrix 2 labels](https://github.com/NacuAndrei/Revenue-predictor/blob/master/Pipeline%20%26%20Statistics/ConfMatrix_RandomForest_2label.png)

- For 4-label classification:

| Label | Precision | Recall | F1 score |  
|-------|-----------|--------|----------|  
| 1.0 | 0.52 | 0.41 | 0.46 |
| 2.0 | 0.47 | 0.62 | 0.53 |
| 3.0 | 0.58 | 0.64 | 0.60 |
| 4.0 | 0.62 | 0.31 | 0.41 |

| Accuracy | Macro F1 score |
|-------|-----------|
| 0.53 | 0.50 |   

![Conf matrix 4 labels](https://github.com/NacuAndrei/Revenue-predictor/blob/master/Pipeline%20%26%20Statistics/ConfMatrix_RandomForest_4labels.png)

For complete results, plots and results analysis, see the [complete documentation](https://github.com/NacuAndrei/Revenue-predictor/blob/master/FullDocumentation.pdf).

# 6. conclusion

We have seen in the Results section that the models chosen tend to perform better in certain situations, but overall, K-Means gave us the best clustering, Random Forest, XGBoost and MLP had the highest F1 score, for classification, and in terms of regression, the two models’ performance is different, for each cluster. 

After analyzing the features in this dataset, we noticed that most of them have a rather low relevance to the revenue. This low correlation might also suggest that the data could be misleading or noisy.

Furthermore, we found out that working with a very large range of numbers, in this case from $7000 up to $780,000,000,000, is very unstable for most models, resulting in poor results. One solution to counteract
this issue seems to be to split this range into smaller dense clusters and also to remove anomalies.

# 7. Useful links
[Complete documentation](https://github.com/NacuAndrei/Revenue-predictor/blob/master/FullDocumentation.pdf)
[My code](https://github.com/NacuAndrei/Revenue-predictor/blob/master/RandomForest_Classification.ipynb)




