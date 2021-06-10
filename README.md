# tag-prediction-nlp
# ⚖ Idenitifying the tags for a legal text document. 
## 1. Problem defination
Create a solution that automatically generate tags for the Test_docs legal text document. Here i have used python and python scikit-learn libraries for text classification.
## 2. Data
The train data contains a total of 80 different samples which are catagorised into 1322 unique tags. The test data has 101 samples to be catagorised.
## 3. Evaluation
  1. Precision
  2. Recall
  3. F1 score

## 4. Features
Some features of the data.
1. There are 1322 unique labels (tags)
2. There are total of 80 sets in training data
3. This is a multilabel classification.

## Getting Data
Data was imported by reading the 80 Train_set, 80 Train_tag and 101 Test_set files. They were then converted to appropriate DataFrames.

## Feature Modelling

We had 1322 total unique tags and the top 50 of them are visualised below. On average each sample had ~2 tags.
![image](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/Tags.png)

After using the NLTK model for tokenizing and lemmanizing the text data, here's how the dataset looked like.

![image](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/dataset.com.png)

The data was then vectorisied using ID-DF, and we can visualise the most frequent words/token used.'court' was found to be the most frequent word in the given text data.

![image](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/token.png)


## Modelling 
While the data is insufficeint for predicting a huge amount of labels, we had only 80 samples. All the text-classification models were failing terribly to predict anything with a score of 0. So I have decided to shorten the enormous amounts of labels present by using clustring Techniques.

  Note: *It is to be noted that the proposed method is just a workaround for this assignment, it does not acturtely predict the exact labels without having more sufficient data*

### Clustering the labels
I used K-Means clustering to cluster the tags, and found that the best k-size was around 250.
![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/cluster_elbow_research.google.com.png)

Here's what the 50 most populated clusters looked.

![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/clusters.png)

After the processing of the tags and the data, the dataframe is shown below for training set.

![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/cluster_df_research.google.com.png)

### Modelling this dataset
Since now we have reduced the tags from 1322 to only 250, we can used classifier models. 


I have used :
 * `KNeighborsClassifier` using OneVsRest (Data Transformation)
 * `RandomForestClassifier` using MulitiOutputClassifier
 * `GaussianNB` Naive Bayes Classifier using ClassifierChain
 * `LinearSCV` using OneVsRest
 The evaluation can be seen below. RandomForestClassifier turned out best.
 ![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/eval_com.png)
 ![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/eval_visual.png)
 
## Predicting on Test data
The labels or the tags based on their clusters were predicted for 101 samples using RandomForest.

![img](https://github.com/OmiWakode/tag-prediction-nlp/blob/main/images/prediction_research.google.com.png)

The full code (notebook) is present in this repository.
