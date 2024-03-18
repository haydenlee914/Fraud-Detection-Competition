# Travelers Insurance Fraud Detection Competition (1st Place)

![image source: Getty Image](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d83aef5-3c28-44c2-be34-4f9c31516a28/Untitled.png)

## *Goal*

The massive size of the insurance industry means that there are more opportunities and bigger incentives for fraud. The total cost of insurance fraud (non-health insurance) is estimated to be more than $40 billion per year. Therefore, we want to build a model that predicts the possibility of a claim being a fraud based on historical claim data.

## *Data*

### Raw Data

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a947670e-dcdd-4e4d-8b67-d06c1465b655/Untitled.png)

Credit card customer data with 17,998 rows and 19 usable columns

- Categorical Variables: 10
- Numerical Variables: 9

### Data Understanding

**Accident location**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b2fd3e26-b1ea-48f4-8c39-acb72ae1e5d9/Untitled.png)

- The data is consist of fraud claims in 5 states; Virginia, Pennsylvania, Iowa, Arizona, and Colorado

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6506b4d0-4af2-4476-811d-2a72e7544b66/Untitled.png)

- Most of the frauds occurred in local

**Histograms**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/67a11d2d-c059-46b4-8ba6-c827992e1859/Untitled.png)

- Red-colored represents a higher number of fraud claims

**Correlation Matrix**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0825da0-0b69-480e-ae57-1a8677338ba3/Untitled.png)

- None of variables have a strong relationship with the target variable (the last row)
- Annual income and Age of driver are strongly correlated in a positive way

## *Data Preparation*

- New variable: Annual income/Age of driver
    - Since these two variables are strongly correlated, annual income is divided into the age of driver to get rid of multicollinearity.
- Transformation
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32a33d2f-6504-41db-b42b-03a00a768bcf/Untitled.png)
    
    - We took log, square root, or cube root to some numerical variables to make sure they are distributed symmetrically
        - This is because we used some distance-based metric for error terms during some of the modeling processes

## *Modeling & Model Evaluation*

- Built decision tree, random forest, support vector machine, XGBoost, and CatBoost regressor
- Using grid search and 3-fold cross-validation, we optimized each model to have the best AUC
- CatBoost model showed the best generalization performance, which is 0.73 of AUC value.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/81f2a2fa-4c33-4ee0-a05c-9cb9858e7993/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/48848afb-1edf-46ff-b81d-9f6b4fb5d975/Untitled.png)

### Feature Importance

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88deb332-7866-4f0b-a6b1-c677a506c616/Untitled.png)

## *Deployment*

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79f48742-cbd0-41f5-9b81-51c089f51705/Untitled.png)

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
