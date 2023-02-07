# Summary of Classifiers tested for Diabetes Prediction

## DataSet

* The RawData file contains 253680 records.
* The data is unbalanced: y=1 has 213703 records (84.2%), while y=2 has
  39977 records (15.8%).
* Training against this unbalanced data skews the results to false
  negatives on positive samples. That means that it will underreport
  people who could be at risk.
* [RandomOverSampling] is used on the training data sets. This
  randomly duplicates postive (y=2) records until the number of
  samples is balanced.

[RandomOverSampling]: https://imbalanced-learn.org/stable/references/generated/imblearn.over_sampling.RandomOverSampler.html

## Random Forest Classifier

* This classifier is prone to overfitting. The parameters must be tuned
  to make sure the prediction accuracy is in line with the accuracy
  against the trained data.
* For example, a classifier with `n_estimators==128` and no `max_depth`
  selected will learn the training sample very well: 95% accuracy. It
  will only predict against the test data at 79% accuracy, and it has a
  positive result recall of only 39%, which means it gives too many
  false negative predictions.
* A balanced model has `n_estimators=48` and `max_depth=8`. That gives
  72% training and prediction accuracy, and returns 77% accuracy for
  positive samples.

## K Nearest-Neighbor Classifier

* This classifier gives decent general accuracy, but poor positive recall. 
  It's also the largest model and fairly slow to train. 
* The best model that was found was `k=75` which had 77% prediction accuracy
  but only 62% positive recall. Higher k values may do better.

## Multi-Layer Perceptron Classifier

* Default settings (1 hidden layer of 100 nodes) give decent results.
  72% prediction accuracy with 77% positive recall. 
* A tuned model (2 hidden layers, 64 and 8 nodes) gives only a slight
  improvement. 73% prediction accuracy with 76% positive recall.
* The trained model is very compact for easy storage and quick evaluation.
* NN models typically want scaled input data. While it improved the
  training time on this model, it did not improve the results. Using
  scaled data also means you have to scale the test inputs when used on
  the website app.

## Conclusions

* The Random Forest classifier provides good results when properly tuned
  against overfitting.
* The MLP classifier is just as good. There's no strong advantage of
  using one over the other.
* The KNN classifier does not perform as well as the other two.

| Classifier | Negative Recall | Positive Recall | Overall Prediction Accuracy | Comment |
| :---          |  ---: |  ---: |  ---: | :--- |
| Random Forest | 71.1% | 77.4% | 72.1% | Best positive recall |
| MLP           | 72.3% | 75.7% | 72.8% | Comparable with RF   |
| KNN           | 79.2% | 62.4% | 76.6% | Poor positive recall = too many false negatives |


