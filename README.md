# Machine Learning: Shipping Prediction Systems
This project is made and presented during Rakamin Academy: Final Project Class.
## Current problems
1. In Indonesia, 34% of customers are not satisfied with experienced of shipment from e-commerce.

2. Most of customer complaints are about late shipping and inaccurate transit time.
![image](https://user-images.githubusercontent.com/85215450/120916181-4354e100-c6d2-11eb-9908-2a53540d8713.png)


## Goals
1. Increase **customer satisfaction**
2. Reduce **Churn customers**
3. Reduce **potential revenue loss**

## Solutions
![image](https://user-images.githubusercontent.com/85215450/120916155-186a8d00-c6d2-11eb-9e59-23fc25d9a388.png)
1. **Prediction**: We try to predict the shipment either they are On Time or Not On Time, it Can help company to make Estimated time of Arrival (ETA).
2. **Shipment**: If the predict turn in to Not On Time, the system will give a warning to shipment section.

## Data Insights

### 1.More important goods _equals_ higher chance to arrive on-time?
It seems **not**. **High important product has the lowest chance to arrive on time**. Low and medium has the same chance to arrive on time, with **the maximum chance of only 40%** .\
![image](https://user-images.githubusercontent.com/85215450/120916273-e4dc3280-c6d2-11eb-9aa4-6eec0cc5a39a.png)\
If this left unchecked, some possible outcomes will happen:\
a) **Customers wont use our service at all.**\
We cant guarantee any satisfying performance (_the chance of any goods will arrive on time is lower than 50%_).\
b) **Customers would opt for lower priority shipping instead.**\
There is _no incentive_ of using shipping option with higher fee.

### 2. How _mode of transportations_ and _warehouse blocks_ affects _the goods arrival_?!
![image](https://user-images.githubusercontent.com/85215450/120916476-07bb1680-c6d4-11eb-821d-6140e488fec9.png)\
Looks like there is **no significant difference** between mode of shipments among different warehouse blocks.

We concluded that the **low chance of on-time arrival is not caused by a specific block or mode of shipment.**

### 3. How is _the discounts_ applied to goods distributed?!
![image](https://user-images.githubusercontent.com/85215450/120916632-f0305d80-c6d4-11eb-9477-0800da7ff0e5.png)\
**Goods which arrived on-time are discounted between 1-10%.**

Goods which **arrived late** are mostly discounted in the same range, but **there are also discounted more than 10% and they are spreaded evenly**.

We assume that products which discounted higher than 10% is sold during special events (i.e. Ramadan big sale).\
![image](https://user-images.githubusercontent.com/85215450/120916789-ab58f680-c6d5-11eb-8a4c-6513d6d6d7e2.png)\
All goods which sold during events  are late. We assume that this is caused by shipment overload during the event.

## Machine Learning Model

### Dataset details
![image](https://user-images.githubusercontent.com/85215450/120916881-6c777080-c6d6-11eb-8339-65a1053c3577.png)

### Data Preprocessing
Things we did before modelling.\
![image](https://user-images.githubusercontent.com/85215450/120916900-929d1080-c6d6-11eb-8706-3dfaf3cd4ebe.png)

### Modelling
We tested several algorithms and the results are presented below.
|             Model           |     Recall    |     Precision    |     Accuracy    |     AUC    |                Feature               |
|:---------------------------:|:-------------:|:-----------------:|:---------------:|:----------:|:------------------------------------:|
|     Logistic Regression     |       69%     |         70%       |        64%      |     63%    |             All   Feature            |
|     KNN                     |       67%     |         71%       |        64%      |     63%    |             All   Feature            |
|     Decission   Tree        |       69%     |         70%       |        63%      |     62%    |             All   Feature            |
|     Random Forest           |       65%     |         75%       |        66%      |     67%    |             All   Feature            |
|     AdaBoost                |       64%     |         78%       |        68%      |     69%    |             All   Feature            |
|     XGBoost                 |       66%     |         76%       |        67%      |     67%    |             All   Feature            |
|     Adjust Decision Tree^   |       76%     |         71%       |        65%      |     64%    |     Drop   Mode shipment & Gender    |

_Notes:_\
^Adjsuted Decision Tree is Decision Tree with some hypertuned parameters and dropped columns said in "Feature".\
All the models are already optimized, including underfitting/overfitting adjustments.

### Evaluation
In all models, we set the positive value as 1 (LATE). Therefore, the confusion matrix is explained like this.

1. True Positive (Reality LATE, Prediction LATE)
2. True Negative (Reality ON-TIME, Prediction ON-TIME)
3. False Negative (Reality LATE, Prediction ON-TIME)
4. False Positive (Reality ON-TIME, Prediction LATE)


In our case, we want to minimalize **False Negative** outcome, because we want to prevent error in predicting goods, which are actually late but the models predict on-time. Therefore, we want our models to focus on **Recall**, which correlate to how small the false negative is.

Based on table, the best model is **Adjusted Decision Tree**, which has the highest Recall.

### Impact
![image](https://user-images.githubusercontent.com/85215450/120918648-a26d2280-c6df-11eb-9fca-80ccd97ce085.png)
![image](https://user-images.githubusercontent.com/85215450/120918837-b6fdea80-c6e0-11eb-883a-6ee55161f353.png)


In conclusion, our models will:
1. Increase customer satisfaction rate by **>76%**.
2. Reduce potential churn customers by **1856** customer.
3. Prevent potential revenue loss by as much as **USD 390,228**.

## Suggestion
**Improvement from internal management**:
Warning notification for product shipping latency.

**Improvement from customers handling**:
1. Add time estimation to customer to lower expectation of time arrival 1- 2 days extra.
2. For ’late-predicted’ product, customer will have shipping voucher on next purchase.   


