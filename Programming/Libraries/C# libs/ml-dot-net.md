# ML .NET

- A Machine learning library for use in C#/.Net

## Machine Learning Tasks in ML.NET
  
### Binary Classification
- Supervised machine learning task that is used to predict which of two classes (categories) an instance of data belongs to. The input of a classification algorithm is a set of labeled examples, where each label is an integer of either 0 or 1.
- The output of a binary classification algorithm is a Classifier which you can use to predict the class of new unlabeled instances. 

- Classification trainers in ML.NET
  - **Averaged Perception Trainer**
  - **SDCA Logistic Regression Binary Trainer**
  - **SDCA Non Calibrated Binary Trainer**
  - **Symbolic SGD Logistic Regression Binary Trainer**
  - **Lbfgs Logistic Regression Binary Trainer**
  - **Light Gbm Binary Trainer**
  - **Fast Tree Binary Trainer**
  - **Fast Forest Binary Trainer**
  - **Gam Binary Trainer**
  - **Field Aware Factorization Machine Trainer**
  - **Prior Trainer**
  - **Linear Svm Trainer**


## Multiclass Classification
- Supervised Machine Learning Task that is used to predict the class (category) of an instance of data. 
- Each label starts as text. It is then run through the Term Transform, which converts it to the Key(numeric) type. 
- Output is a classifier.

- Trainers include:
  - **LightGbmMulticlassTrainer**
  - **SdcaMaximumEntropyMulticlassTrainer**
  - **SdcaNonClibratedMulticlassTrainer**
  - **LbfgsMaximumEntropyMulticlassTrainer**
  - **NaiveBayesMulticlassTrainer**
  - **OneVersusAllTrainer**
  - **PairwiseCouplingTrainer**


## Regression
- Supervised Machine Learning task that is used to predict the value of the label from a set of related features. The label can be of any real value and is not from a finite set of values as in classification tasks. 
- Regression algorithms model the dependency of the label on its related features to determine how the label will change as the values of the features are varied.

- Trainers: 
  - **LbfgsPoissonRegressionTrainer**
  - **LightGbmRegressionTrainer**
  - **SdcaRegressionTrainer**
  - **OlsTrainer**
  - **OnlineGradientDescentTrainer**
  - **FastTreeRegressionTrainer**
  - **FastTreeTweedieTrainer**
  - **FastForestRegressionTrainer**
  - **GamRegressionTrainer**

## Clustering
- Unsupervised machine learning task that is used to group instances of data into clusters that contain similar characteristics. Clustering can also be used to identify relationships in a dataset that you might not logically derive by browsing or simple observation. 

- Trainers: 
  - **KMeansTrainer**

## Anomaly Detection
- The task creates an anomaly detection model by using Principal Component Analysis (PCA). PCA-Based Anomaly Detection helps you build a model in scenarios where it is easy to obtain training data from one class, such as valid transactions, but difficult to obtain sufficient samples of the targeted anomalies.

- PCA is frequently used in exploratory data analysis because it reveals the inner structure of the data and explains the variance in the data. PCA works by analyzing data that contains multiple variables. It looks for correlations among the variables and determines the combination of values that best captures differences in outcomes. 

- Trainers: 
  - **RandomizedPCATrainer**

## Ranking
- A ranking task constructs a ranker from a set of labeled examples. 
- Trainers:
  - **LightGbmRankingTrainer**
  - **FastTreeRankingTrainer**

## Recommendation 
- A task that enables producing a list of recommended products or services. 
- Training:
  - **MatrixFactorizationTrainer**

## Forcasting
- task use past time-series data to make predictions about future behavior.
- Trainers:
  - **ForcastBySss**

## Image Classification
- supervised machine learning to predict the class of an image.

- Trainers:
  - **ImageClassificationTrainer**

