# Multi-label Classification

Three approach's

Binary Relevance: the ensemble of labels is split and then trained in a binary fashion for each label 
- con: it does not take label correlation into consideration
- low computational cost. 

Label powerset: combines multilabel into a two part single label and trains based on that

pro: it takes label correlation into consideration 
con: high computational complexity can lead to imbalanced dataset with multiple classes associated with few examples 

Classifier chain: model learns classifiers as in binary relevance method however all classifiers are linked in a chain

pro: label correlation taken into consideration, acceptable computational complexity 
con: accuracy heavily depends on the order, for n labels there are n! possible orders 


MLkNN: is a binary classifier that's modified to conform to multilabel predictions: 
pro: better accuracy than the previous methods, correlations between labels are considered 
cons: with the binary relevance the ratio estimation may not be accurate, data distributions for some labels are imbalanced