# :money_with_wings: Overview of the loan prediction risk analysis:
LendingClub is a peer-to-peer lending services company that has a credit card credit dataset.  This project uses various techniques of oversampling, undersampling, and combination-sampling (bias reduction) approaches to predict credit risk.  

## :credit_card: Purpose and Definitions of this analysis:
The purpose is to evaluate the performance of these models and make recommendations on whether they should be used to predict credit risk.

- **True Positive (TP)** means that high risk is predicted, and the loan is truly high risk.
- **True Negative (TN)** means that low risk is predicted, and the loan is truly low risk.
- **False Positive (FP)** means that high risk is predicted, but the loan is actually low risk.
- **False Negative (FN)** means that low risk is predicted, but the loan is actually high risk.
 
**pre = Precision = TP/(TP+FP).**  
- When the ratio of correctly predicted high risk loans to the total number of high risk predictions is high, then precision should be high.  
- When there are too many false positives, precision will be low.  

**rec = Recall = TP/(TP+FN).**  
- It is also known as Sensitivity.  
- It reflects the ratio of correctly predicted high risk loans to the total actual high risk loans.  Thus, a low recall means a lot of false negatives, and a high recall means a lot of true positives.  
- False negatives are a concern because they are actually high risk loans that went undetected and marked as low risk.  The Lending Club would want to look carefully at this metric because in this case, it is better to err on the side of excluding qualified applications than to accidentally let in applications that are actually high risk.

**spe = Specificity = TN/(TN+FP).**  
- Specificity reflects the True Negative Rate.  
- It is the ratio of correctly predicted low risk loans to the total actual low risk loans.  
- This should be less of a concern to the Lending Club, given that most of what they have is low risk.

**f1 = F1 Score = (2 * Precision * Recall/(Precision + Recall)).**  
- This is essentially a weighted average of Precision and Recall, with 1.0 being the best true positive rate.

**geo = Geometric Mean = sqrt(Recall * Specificity).**  
- This may be useful to examine the square root of the product of both true positives and true negatives.

**iba = Index Balanced Accuracy =  (1 + alpha * (Recall - Specificity)) * (Recall * Specificity).**  
- It measures performance.  
- Alpha refers to the True Positive rate minus True Negative rate. 

**sup = Support**

Reference:
[Supplemental Source for Definitions](https://dev.to/amananandrai/performance-measures-for-imbalanced-classes-2ojj)


## :moneybag: Results:

### Balanced accuracy score and the precision and recall scores of all six machine learning models

**1. Naive Random Oversampling**
- Accuracy: .6439
- High Risk Precision: .01
- Recall: .69
- This is eliminated because of relatively low balanced accuracy and .01 high risk precision. The recall is also not among the better models.  
![1](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/1Naive_Random_Oversampling.png)



**2. SMOTE Oversampling (Synthetic Minority Oversampling Technique)**
- Accuracy: .6629
- High Risk Precision: .01
- Recall: .63
- This is eliminated because of relatively low balanced accuracy and .01 high risk precision. The recall is also the worst of all the models.
![2](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/2Smote_Oversampling.png)



**3. Cluster Centroids Undersampling**
- Accuracy: .5443
- High Risk Precision: .01
- Recall: .69
- This is eliminated because of its lowest balanced accuracy among all models and .01 high risk precision. The recall is also not among the better models.
![3](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/3Cluster_Centroids.png)



**4. SMOTEENN (Synthetic Minority Oversampling Technique with Edited Nearest Neighbor Undersampling)**
- Accuracy: .6748
- High Risk Precision: .01
- Recall: .76
- This is eliminated because of relatively low balanced accuracy and .01 high risk precision. The recall is the second best among all models, so it could be a third choice after the next two, but it's not ideal.
![4](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/4SMOTEENN.png)



**5. Balanced Random Forest Classifier**
- Accuracy: .7885
- High Risk Precision: .03
- Recall: .70
- This model has the second highest balanced accuracy and .03 high risk precision which is higher than the prior 4 models. The recall is the third best among the models.
![5](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/5Balanced_Random_Forest_Classifier.png)



**6. Easy Ensemble AdaBoost Classifier**
- Accuracy: .9317
- High Risk Precision: .09
- Recall: .92
- This has the best balanced accuracy score and the best high risk precision score and the best recall, so it is the clear best model overall.
![6](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/6Easy_Ensemble_AdaBoost_Classifier.png)



## :heavy_dollar_sign: Summary of Six Models:
![Table1](https://github.com/Super-Manda/Credit-Risk/blob/main/Images/Table1.png)

### Results Summary:
- For balanced accuracy score, the Easy Ensemble with Adaptive Boost is the highest at 0.9317, and no other model really comes close, because the next highest is the Balanced Random Forest at 0.7885.  

- For high risk precision, no model is truly recommendable in the sense that they range from 0.01 to 0.09, so all models are considered to have too many false positives, but of these, the one that is the most precise among them would be the Easy Ensemble with Adaptive Boost at 0.09.  

- Since precision is not a deal breaker in this industry, and recall is more important, it is noted that the Easy Ensemble with Adaptive Boost has the highest recall and that no other model comes close.   

- When looking at the weighted average of precision and recall (the F1 score), the Easy Ensemble with Adaptive Boost is the highest with a score of 0.16.  So one may want to use the Easy Ensemble with Adaptive Boost method, but then also go through the results with a finer-tooth comb after it to do some type of post-hoc analysis that would make it a better model for high risk precision, since 0.16 is hard to justify using on its own.  To do this, perhaps the Lending Club could make some kind of "loan appeal process" such as, if you feel that your application was denied in error, please contact the Lending Club.  This way, if people can show their actual credit-worthiness on appeal, it would bring up the prcision value.

## :chart: Recommendations:
- Out of these six models, the Easy Ensemble AdaBoost Classifier Model is the most successful that should be used in conjunction with some kind of Lending Club appeals process, which could strengthen its precision in the future.  The next most successful as a backup choice would be the Balanced Forest Classifer model because it has the next lowest rate of false low risk and the next highest accuracy, but this one is clearly not as good as the Easy Ensemble-- it'd be more of a second best choice if needed.  

- The least successful is the Cluster Centroids.  That model should definitely not be used because there is no metric for which it provides good results.

- In general, the models with lowest accuracy and precision are the first 4 models, which can also be eliminated.
