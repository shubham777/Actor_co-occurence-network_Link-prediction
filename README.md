# Actor_co-occurence-network_Link-prediction

## Overview:
Link prediction is a widely studied task in network science and machine learning, where the goal is to predict the likelihood of a missing or future edge between two nodes in a network. In this repository, we present an approach for link prediction in an actor co-occurrence network, where each node corresponds to an actor and the edges denote co-occurrence on the same Wikipedia page. Our method leverages both graph structure and node attribute features to predict missing or future edges in the network. 
To predict missing or future edges between actor nodes in the co-occurrence network, we experimented with several machine learning models, including random forest, extra tree, XGBoost, and logistic regression. We trained each model on a combination of graph structure and node attribute features and evaluated their performance using various metrics, such as accuracy, precision, recall, and F1 score. Our experimental results show that the logistic regression classifier outperformed the other models in terms of prediction accuracy, achieving a score of 0.75695. Our approach has the potential to be applied to other types of networks and can be used in a variety of practical applications, such as recommendation systems and network reconstruction.

## Dataset
The directed graph is an actor co-occurrence network that is comprised of 10k node pairs where edges represent co-occurrence on the same Wikipedia page.

## Methodology
### Graphs creation
We populated an empty graph with nodes from the node features file to use the data graph structure. Each node had a dictionary of features. We added edges from the training data with a label of 1 to the graph using the add edges from() function. We removed graph self-loops. This graph was created to help us understand actor relationships and compute powerful embeddings that represent the subject and environment of Wikipedia pages.

![image](https://user-images.githubusercontent.com/127759119/235368774-e6c97eb2-fa58-4fe4-ab12-7edc259e7bcf.png)

### PageRank Scores:
We used a function called nx.pagerank() from the NetworkX library to calculate scores for the different nodes in the graph. The alpha parameter is set to 0.8 for calculating random walk PageRank scores.

### Other feature generration
For each missing edge, the following features are extracted:
• Random walk similarity
• Degree centrality for the source node
• Degree centrality for the target node
• Clustering coefficient for the source node
• Clustering coefficient for the target node

### Models
This study fine-tuned several models using training/validation sets created after scaling the data. We tried Random Forest, Extra-tree Regressor, XGBoost, and Logistic Regression. When fine-tuning one model, we experienced significant computational delays. We assessed each model’s performance and computational efficiency. XGBoost, Logistic Regression, and Extratree models outperformed the others after several experiments. Thus, we concentrated on fine-tuning and using these three
models.

## Models Comparison
### Accuracy: 
Among the models, the Logistic regression model has the highest accuracy score of 0.7642, outperforming the others. The Xgboost and Extra-tree regressor models have (respectively) moderately high accuracy scores of 0.7543 and 0.7429
### F1 Score: 
The F1 score, which is a measure of the balance between precision and recall, shows that the Logistic Regression Model also has the highest score of 0.7607, significantly outscoring the other models. Xgboost has the second highest F1 score of 0.7568. and the Extra-Tree Regressor model has the lowest F1 score of 0.7236.
### AUC Score: 
The AUC score, which indicates the model’s ability to distinguish between positive and negative samples, is also highest for logistic regression, followed by the Xgboost with a score of 0.7546 and the Extra-Tree Regressor with a score of 0.7453.

