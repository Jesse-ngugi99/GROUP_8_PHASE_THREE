# CHURN ANALYSIS 
***
![alternative](./images/churn.png)
## BUSINESS OVERVIEW
Telecom companies provide phone, internet, and mobile services. The industry keeps changing with new tech like 5G, higher customer expectations and stiff competition from related fields . The Telecom companies support many sectors such as e-commerce, fintech, and biotech, all of which depend on digital systems and data. Syriatel like many telecom companies has often faced  challenges such as customer churn where the clients cancel subscriptions and leave for competitors or even fraud. To stay competative, the companies must solve problems quickly and use data to guide decision.

## BUSINESS PROBLEM
Telecom companies like Syriatel, customer churn is a big risk to revenue and market share. Without knowing why customers leave, the company cannot act in time to keep them. The main goal of this project is to use the customer data to build a predictive model that identifies customers likely to leave, helping Syriatel improve retention, reduce revenue loss, and support long-term growth

## DATA
* The dataset used for this project is from Kaggle.[data](https://www.kaggle.com/datasets/becksddf/churn-in-telecoms-dataset)
* It consists of 3333 records and 21 columns.
* The dataset consists of float, integer, boolean, and object data types.
* The dataset contains information on customer data across different states, including their usage behavior, subscription plans, and churn status.
The column names are:
1. State -state where the customer resides
2. Account length -Period the customer has had the account for.
3. Area code -Telephone area code of the customer
4. Phone number - Customer's telephone number
5. International plan -Whether the customer has an international calling plan (yes/no)
6. Voice mail plan -Whether the customer has a voice mail plan (yes/no)
7. Number vmail messages -Number of voicemail messages sent or received
8. Total day minutes - Total minutes of calls made during the day
9. Total day calls - Total number of calls made during the day
10. Total day charge - Total charges for daytime calls
11. Total eve minutes-Total minutes of calls made during the evening
12. Total eve calls -Total number of calls made during the evening
13. Total eve charge -Total charges for evening calls
14. Total night minutes -Total minutes of calls made during the night
15. Total night calls -Total number of calls made during the night
16. Total night charge -Total charges for night calls
17. Total intl minutes -Total minutes spent on international calls.-
18. Total intl calls -Total number of international calls.
18. Total intl charge - Total cost charged for international calls.
19. Customer service calls-Number of times the customer called customer service.
20. Churn -Whether the customer left the company

* Doing futher ivestigations to our dataset we realsed; there are there are no duplicate records and no missing values.
* The target column is churn.
     
## METHODS
This project uses descriptive statistics and predictive modelling to provide insights into customers churn.

## RESULTS
* Plotting the a correlation matrix with the target column, we figured customer service calls, total day minutes and total day charge are the top correlated features to churn.
  
![alternative](./images/Targetcorrelationmatrix.png)

* And since total day charge and total day minutes are collinear  we removed one to prevent multicollinearity in the model

![alternative](./images/TotaldayminutesvsTotaldaycharge.png)

* Comparing churn rate by international plan; Customers with an international plan show a higher likelihood of churn compared to those without. 
  
![alternative](./images/churnratebyinternationalplan.png)

* Churn rate by customer service calls; Customers who frequently contact customer service are more likely to churn

![alternative](./images/churnratebycustomerservicecalls.png)

* Churn rate by voice mail plan; Customers with a voice mail plan have a lower churn rate compared to those without
  
![alternative](./images/churnratebyvoicemailplan.png)

* The target column "churn" appeared to be imbalanced with many non-chuners(class 0) compared to chuners(class 1)

![alternative](./images/churndistribution.png)

* Since the target variable (churn) is binary, this is a classification problem, so we applied logistic regression as the baseline model.
  
#### **Logistic Regression (before class balancing)**

* The model has 828 True negatives meaning out of 855 non-churners it correctly predicted 828 non-churners
* The model has 38 True positives meaning out of 145 churners it correctly predicts 38 churners
* The model has 107 False negatives meaning model wrongly classified 107 churners as non-churners
* The model has 27 False positive meaning it wrongly classified 27 non-churners as churners

![alternative](./images/logregcfmbeforebalancing.png)

* The model has an accuracy of about 87%
* Precision for class 0(non-churners): suggests the model is correct 89% of the times it predicts non-churners.
* Recall for class 0 (non-churners): indicates the model captures 97% of actual non-churners.
* Precision for class 1 (churners: The model is correct 58% of the times it predicts churners.
* Recall for class 1 (churners): The model captures 26% of actual churners

* From the above inferences the model is biased towards the majority class(non-churners). Since class 0 (non-churners) outnumber class 1 (churners) this means the model tends to favor predicting non-churn more often, leading to poor performance on churn detection.

#### **Logistic Regression (after class balancing)**

![alternative](./images/logregafterbalancing.png)

* The model has 655 True negatives sugesting out of 855 non-churners the model correctly predicts 655 non-churners
* The model has 108 True positives meaning out of 145 churners the model correctly predicts 108  of churners, compared from the previous model there is a slight improvement in the model predicting the churner class now.
* The model has 37 False negatives meaning the model wrongly detects 37 churners as non-churners
* The model has 200 False positive indicating that the model wrongly classified 200 non-churners as churners

* After class balancing, the model achieves about 76% accuracy, correctly predicting churn for 76% of customers. 
* Precision for class 0(non-churners), the model is correct 95% of the times it predicts non-churners
* Recall for class 0 (non-churners), the Model captures 77% of actual non-churners
* Precision for class 1 (churners), the model is correct 35% of the times it predicts churners
* Recall for class 1 (churners): The model captures 74% of actual churners

**Recall for churn changed from 0.26 to 0.74, meaning the model catches most churner now but with more false positives**.

This adjustment is acceptable in this churn analysis because missing a churner is more costly than wrongly predicting a non-churner as churner.

![alternative](./images/logregroccurve.png)

* The curve shows how recall and specificity change at different thresholds.
* An AUC of 0.82 indicates the model performs fairly good at separating churners from non-churners. In practical terms, if we randomly pick one churner and one non-churner, the model has an 82% chance of giving the churner a higher score.
* Overall, the model is fairly reliable in detecting customer at risk of churn.
* The higher the AUC means the better separation between churners and non-churners.

* We proceed to build the next model to see if the perfomance will improve.

#### **Decision Trees (before class balancing)** 

![alternative](./images/dtcfm.png)

* The model has 853 True negatives meaning the model correctly predicted 853 non-churners out of 855 non-churners
* The model has 114 True positives, meaning out of 145 churners the model correctly predicts 114.
* The model has 31 False negatives meaning the model wrongly detected 31 churners as non-churners
* The model has 2 False positive meaning it wrongly classified 2 non-churners as churners

* The model has an overall accuracy of 96.7%. 
* Class 0 (non-churners): Very high recall (100%) and precision (96%), meaning almost all non-churners are correctly identified.
* Class 1 (churners): Precision is high (98%) but recall is lower (79%), while most predicted churners are correct, some actual churners are missed.
  F1-scores: 0.98 for non-churners, 0.87 for churners indicating the model performs better for non-churners at this point.

![alternative](./images/dtb4classbalance.png)

* The tree shows Customer service calls, total day charges, international plan as the main churn contributors.
Most churners are customers who:
1. Frequently Seek support from customer services
2. Have higher international charges
3. Have an international plan

#### **Decision Trees (after class balancing)** 

* The model has an accuracy of 91%, meaning the model correctly predicts churn for 91% of the customers.
  
![alternative](./images/dtcfm2.png)
* Confusion matrix; Out of 145 actual churners, 117 were correctly predicted, while 28 were missed. Among 855 no-chuners, 61 non-churners were incorrectly predicted as churners and 794 non-churners correctly predicted as non-churners.
* Looking at the confusion matrix Non-churners (Class 0) have a High precision (97%) and recall (93%), meaning most non-churners are correctly identified.
* Churners (Class 1) have Lower precision (66%) but a good recall (81%) compared to the recall of the previous decision tree before balancing the class using SMOTE, meaning this final model performed much better at catching churners.
  
![alternative](./images/dtroccurve.png)

* The AUC of 0.88 is significantly high indicating that the Decision Tree model correctly distinguish churners from non-churners 88% of the time.
  
![alternative](./images/dtafterclassbalance.png)


## CONCLUSIONS
* Customers who frequently contact customer service are more likely to churn, while those with few service calls are less likely to leave. This suggests that repeated calls may reflect dissatisfaction or unresolved issues.

* Customers with high service calls combined with high daytime charges strongly increase the likelihood of churn, pointing to an important churn pattern.
  
* Customers without a voice mail plan and with high daytime charges are more likely to churn. On the other hand, those with a voice mail plan and high daytime usage are more likely to stay, suggesting that the voice mail plan adds value and increases satisfaction.
  
* Customers who have an international plan and high daytime charges are also at a higher risk of churning, possibly because of high costs or unmet expectations with international services
  


## RECOMMENDATIONS
1. The company should improve customer service, as frequent support calls may signal unhappy customers. The company can consider reviewing the customer service workflow to resolve issues faster this can help reduce repeated calls.

2. Company should come up with a retention plan for international users since customers with international plans combined with high daytime usage are more likely to churn. The company can create special offers, discounts, or loyalty rewards for these customers.

3. Promotion of voicemail plans: Regular daytime callers without voicemail plans are more likely to churn. Offering bundled promotions for voicemail could help retain these customers.”
 
4. The company should proactively engage high-usage customers with check-ins or small perks to make them feel valued and lower churn risk

5. The company should use targeted communication, like personalized messages and tailored offers, to encourage customers at risk of churn such as frequent callers or heavy international users to stay

6. High daytime and international charges may frustrate customers. The company could review the charges and offer flexible packages to reduce customers frustation.

7. Some customers may not fully understand their plan benefits. Educating them—for example, showing how voicemail or bundled offers save money can improve customer retention.

****

## Repository Structure
```
├── images
├── gitignore
├── README.md
├── fims_analysis.ipynb
└── presentation.pdf
```
