# Travelers Insurance Fraud Detection Competition (1st Place)

![image source: Getty Image](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/e049f3dd-01bb-4e09-b0e5-ca8396037db3)

## *Goal*

The massive size of the insurance industry means that there are more opportunities and bigger incentives for fraud. The total cost of insurance fraud (non-health insurance) is estimated to be more than $40 billion per year. Therefore, we want to build a model that predicts the possibility of a claim being a fraud based on historical claim data.

## *Data*

### Raw Data

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/0ffc6b86-e94c-41da-b88e-0dc39c6d32e7)

Credit card customer data with 17,998 rows and 19 usable columns

- Categorical Variables: 10
- Numerical Variables: 9

### Data Understanding

**Accident location**

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/236eed02-325f-4087-9b92-23b9c6041a39)

- The data is consist of fraud claims in 5 states; Virginia, Pennsylvania, Iowa, Arizona, and Colorado

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/b15dc7c6-52ac-4055-a4ef-5b63f983557b)

- Most of the frauds occurred in local

**Histograms**

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/a5b9df62-4834-4776-8818-d0c51e2af679)

- Red-colored represents a higher number of fraud claims

**Correlation Matrix**

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/87fbf16d-21a4-4046-9aff-10ffa4fc31d5)

- None of variables have a strong relationship with the target variable (the last row)
- Annual income and Age of driver are strongly correlated in a positive way

## *Data Preparation*

- New variable: Annual income/Age of driver
    - Since these two variables are strongly correlated, annual income is divided into the age of driver to get rid of multicollinearity.
- Transformation
    
    ![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/f816a148-602f-4e75-bbdb-0479bf7abfb0)
  
    - We took log, square root, or cube root to some numerical variables to make sure they are distributed symmetrically
        - This is because we used some distance-based metric for error terms during some of the modeling processes

## *Modeling & Model Evaluation*

- Built decision tree, random forest, support vector machine, XGBoost, and CatBoost regressor
- Using grid search and 3-fold cross-validation, we optimized each model to have the best AUC
- CatBoost model showed the best generalization performance, which is 0.73 of AUC value.

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/3395f849-5701-49bd-8f5a-04b81c46eb2d)

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/d9c81bd9-ca4f-4dc5-b390-0522da685998)

### Feature Importance

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/ba6e2ee6-c491-4c59-9ddc-fc7729fe8844)

## *Deployment*

![Untitled](https://github.com/haydenlee914/Fraud-Detection-Competition/assets/140643142/8716f17c-292b-4523-9486-388cb25cce3c)

- Dealing with fraud can be time and resource-consuming for the company, squandering profits.
- Estimated model value will be around $3,000 per claim, combining cost & benefit matrix and confusion matrix

## ***Risks and Challenge***

1. Fraud detection, in reality, cannot be easily interpreted as a binary classification problem. It is likely to be a multi-class classification problem since there are so many types of fraud, and the techniques people use for conducting fraud are evolving over time. So it is necessary for the company to be sensitive about their techniques and update the types of data collected, and more importantly the model all the time.
2. In the real world, the data is unlabeled, meaning we don’t know the classification. In this case, it might be more suitable to use unsupervised learning. If we used unsupervised learning, we need experts that have the domain knowledge to confirm our prediction results.
3. Even if we can use supervised learning to build models based on historical data, due to the variety of fraud and its speed of changing, the model might not work well in practice. At least we cannot depend only on one model to predict all kinds of fraud. We need to have a good understanding of all types of fraud and the types of data needed specifically for each type of fraud.
4. It is hard to distinguish between noise and anomaly. It might require objective judgments sometimes.

## *Future Improvement*

1. Time series analysis to detect any seasonal pattern
2. Statistical test to check if a significant difference exists between the fraud records and the non-fraud records
3. Unsupervised learning for unlabeled data, such as GMM(Gaussian Mixture modeling) and isolation forest to potentially detect fraud
4. Social network analysis to get more information on customers' behavior or capture clues of new fraud techniques
