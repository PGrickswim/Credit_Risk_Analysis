# Credit_Risk_Analysis

## Overview
This analysis seeks to leverage existing data around credit risk to determine creditworthiness based on many factors. The data will be fed into six machine learning models which will each be shown based on accuracy score, precision, and recall. To start, an explanation of precision and recall is shown below

### Precision
Precision describes how likely a value is likely to be positively predicted. When the model anticipates a positive or true outcome, and it is actaully true, that is considered a "True Positive". When the model predicts a True outcome but the actual situation is false, that's called a False Positive. Precision is calculated by dividing True Positives by the sum of True Positives and False Positives.

In our case of creditworthiness, a true value would be a high-risk loan, which means that a True Positive occurs when the model accuarately surfaces a risky borrower. A Fale Positive result occurs when the model predicts a risky borrower, but the loan is acutally not a risky loan. From a business point of view, denying lending to borrowers who are not risky is not dangerous, but it is bad for business. Furthermore, individuals a weak model may expose as risky are likely to be the same borrowers that would be likely to accept an offer of lending at a higher interest rate, which so long as the loan does not default, is more profitable to the lender. 

### Recall

Recall, also known as sensitivity, answers the question, "If i know something is true, how likely is it that the model predicts it?" So in our case, recall is testing to see how the number of true positives (accurately predicted risky borrowers) compares to the number of false negatives, which are risky borrowers that were not predicted as such by the model. 

In our case of creditworthiness, false negatives are the quadrant we really want to avoid. False Negatives are those that, based on model output, would be offered credit, but then would default on the loan. This is costly and definitely bad for business and very costly to the company

### Other Considerations

Based on the lender's financials, it would be important to determine the imporantce of recall in light of precision flaws. For example, if the company knows that the average default is 10 times as costly as a good loan is profitable, we would want to know that the model is that much more likely to offer a loan to a borrower who may have some baggage but will in the end pay, than to a borrower who will default.  Put another way, the company would be comfortable with some False Negatives (defaults) as long as they are far outweighed by the number of True Positives, and would want assurances that True Positives are inclusive of higher-profit-margin loans that will not default. 

## Our Models / Analysis

For each of the below, an image showing the code output for the accuracy score and confusion matrix is shown, with bullet points showing Balancesd Accuracy Score, the Precision (TP/(TP+FP)),  and Recall (TP/(TP+FN)) of the model. Below this, a summary follows

### Random OverSampling

![Random OverSampling](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/Random_OverSampler.png)

- Balanced Accuracy Score: .65730
- Precision: .01046
- Recall: .71287
- Notes: Terrible Precision, denying a lot of good loan oppotunities.

### SMOTE OverSampling

![SMOTE OverSampling](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/SMOTE_OverSampler.png)

- Balanced Accuracy Score: .66225
- Precision: .01196
- Recall: .63366
- Notes: Terrible Precision, denying a lot of good loan oppotunities. Also, lower recall score here.

### Cluster Centroids UnderSampling

![Cluster Centroids UnderSampling](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/Cluster_Centroids_UnderSampler.png)

- Balanced Accuracy Score: .54422
- Precision: .00675
- Recall: .67327
- Notes: Really bad. Almost zero precision, and again, a recall score under .7

### Combination Sampling with SMOTEENN

![Combination Sampling with SMOTEENN](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/SMOTEENN.png)

- Balanced Accuracy Score: .66225
- Precision: .00939
- Recall: .65347
- Notes: Terrible Precision, denying a lot of good loan oppotunities. Also, lower recall score here.

### Balanced Random Forest Ensemble

![Balanced Random Forest Ensemble](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/Balanced_Random_Forest.png)

- Balanced Accuracy Score: .78855
- Precision: .03192
- Recall: .70297
- Notes: Much improved over under/over/balanced sampling models, but still unacceptably low precision and iffy-at-best recall

### Easy Ensemble

![Easy Ensemble](https://github.com/PGrickswim/Credit_Risk_Analysis/blob/main/Resources/Easy_Ensemble.png)

- Balanced Accuracy Score: .93166
- Precision: .08643
- Recall: .92079
- Notes: Far from perfect, but definitely much improved over the others. See summary

## Summary
Five of the six models are non-starters based on our data set and the important work of determining credit-worthiness. This is due to the recall rates near 70%. This means that when the model is presented with a defaulting loan, 3 times out of 10 the model would choose to offer the lender credit. Comvine this with an at-best 0.03192 sensitivity rate, meaning many good borrowers would be denied credit, and the machine learning does not seem to be a good route to utilize. 

However, the Easy Ensemble method does a much better job in sensitivity, but more importantly at recall. A recall score (as well as a balanced accuracy score) of over 0.9 indicates that it is unlikely to offer credit to a risky borrower. While the number of "no" decisions will still avoid offering credit to 9 out of 10 good borrowers, it is important to note the industry norms and take a look at how this data compares to default rates across the trade.

Suggestion: Use the Easy Ensemble model.