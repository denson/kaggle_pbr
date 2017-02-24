blending demo
==========

I started with emanuele's code and switched to data generated with scikit's "make classification" algorithm. I also added a Jupyter notebook.


The general concept is that if we build multiple different models trained on different samples of our training data we get multiple predictions that are substantially better than chance and that are uncorrelated with each other.


In step 1 we take stratified fold samples of our training data and build multiple models (in this case RDF entropy,RDF-gini ET-entropy,ET-gini and GBT) on each fold. We then use the trained models to predict the training sample not in the training part of this fold. It is super important that you do not use a given model to predict training data that was used to train that model on that fold. We also predict all the test data with each model. These predictions are a way of transforming the training data and the test data into a different space with the predicted probabilities as the transformed information. We take a simple average of the predictions of each type of model (eg RDF-gini) and that becomes the transformed data for the next step. If we have 5 different models as in this case our input data for step 2 will have 5 columns and the same number of rows as the training set and test set respectively.


In step 2 we use a train a logistic regresson on the transformed training data and use it to predict the transformed test data. We take the predicted probabilities from the logistic regression as our final answer.


This method usually results in an improvement over a single highly tuned model for "hard" problems and not "simple" problems. By hard I mean that the decision boundary between classes is highly non-linear. Overlapping classes and non-linear relationships between features contribute to making problems hard.


This academic paper describes the concept:

[Stacked Regressions](http://statistics.berkeley.edu/sites/default/files/tech-reports/367.pdf "Stacked Regressions")


I found this at Kaggle:

[Kaggle competion question](https://www.kaggle.com/c/bioresponse/discussion/1765 "Kaggle forum")

