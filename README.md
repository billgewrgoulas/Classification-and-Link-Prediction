# Classification-and-Link-Prediction

## Part 1 - Classification

The focus of the first part of this assignment is to test some classification algorithms using the [Yelp](https://www.yelp.com/dataset) academic dataset. We will use the classifiers: <b>K Nearest Neighbors, Support Vector Machine, Logistic Regression</b>. From the data we will keep only the reviews for the businesses located in Boston and were made in 2020. Our goal will be to train the classifiers such that for a random review to predict if it's negative or positive. A review with 4 or 5 stars can be assumed to be positive.

### Steps
* In the first step we will use the TfIdf representation of the reviews. For the evaluation we will apply the [KFold](https://scikit-learn.org/stable/modules/cross_validation.html) method to get 5 train-test subsets. For each fold we will create a different TfIdf of the train set and one for the test set, since the representation is related to the subsets. Afterwards we will test the classifiers on the test subset. In addition for the Logistic regression we will extract the 20 features with the worst and best weights in the last fold.
* In the second step we will repeat the first step but this time we will use Google's word embeddings to extract the features. The representation of the reviews will be the average of the embeddings of the words.
* We will evaluate our models using exclusively the mean <b>Confusion Matrix</b> across all 5 folds for each classifier and then calculate the Mean Precision, Recall, F1 scores per class as well as the overall accuracies.

<p align="center"><img src='https://github.com/billgewrgoulas/Classification-and-Link-Prediction/blob/main/B04223_10_02.jpg'></p>

## Part 2 - Link Prediction

In the second part the goal will be to predict the connections that will occur in the future and make the corresponding friend recommendations.
For this purpose we will utilize the [PageRank](https://en.wikipedia.org/wiki/PageRank) algorithm from the [NetworkX](https://networkx.org/) library. The input will be a directed graph that represents a social network.

### Steps
* In the first step we will have to create the train - test sets. The idea is to remove some edges (x, y) from the initial directed graph and store them as the test data. Our goal will be to find the edge that we removed. For the node x the candidate nodes y are all nodes that are not already it's neighbors - set C(x).
* In the second step we will run the PageRank for each node x in the removed nodes and use a personalized PageRank vector such that all the random walks performed by the algorithm will restart from node x. We will repeat this process for a number of different jump probabilities in order to find the optimal value of alpha. For the evaluation we will use the metrics [MRR, MRM, Hits@k](https://pykeen.readthedocs.io/en/stable/tutorial/understanding_evaluation.html) using the ordered C(x) set generated by the algorithm.
* For a better comparison we will also implement two simple algorithms: <b>Neighbor Jaccard Similarity and Common Neighbors</b> and repeat the evaluation process.
* Lastly we are going to test all 3 algorithms on the undirected version of our graph and compare the results.
