# Churn scoring

#### Definition

Churn scoring is a process to predict which customers might stop using a service or buying products from a business, so the business can take steps to keep them.

#### Benefits

Helps a business know which customers are at risk of leaving. This way, the business can reach out to those customers with special offers or improved services to try and keep them around.

## Example of churn analysis and scoring for e-commerce

**Data:** [E_Commerce_Dataset.xlsx](./E_Commerce_Dataset.xlsx)

**Notebooks:** [Churn_Scoring](./MADT8101_Churn_scoring.ipynb)

**Google colab:** [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AsmaMora/MADT8101/blob/main/3.Churn_Scoring/MADT8101_Churn_scoring.ipynb)


## Dataset overview

The dataset is the customer information of e-commerce include 5,630 rows and 20 columns. The details of each columns are as per the table below.

![image](https://github.com/AsmaMora/MADT8101/assets/132048257/f118a25b-a2b9-461a-a96f-8b8aad6c25ea)

## Sanity check and clean raw data
1. **Check missing value** Total rows of the dataset are 5,630 rows and have null value in columns Tenure, WarehouseToHome, HourSpendOnApp, OrderAmountHikeFromlastYear, CouponUsed, OrderCount and DaySinceLastOrder

    Clean data: Remove row which have null column.

## Expore raw data
1. No.of customer by churn flag
   
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/634d2ed8-ef37-4d7b-88db-1c243c4c2519)

2. Avg. No. of device registered by Churn
   
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/95efb1d6-da71-4433-8e90-f2330bf7aa72)
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/1e899fe1-d221-4923-8e6a-9f4cef1feb1f)

3. Avg. Satisfaction score by Churn
   
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/24fbce11-198e-4957-9cf6-76fb894a5fc6)
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/55b872a0-6df4-40af-a8ca-aee1035b32af)


4. Preferred login device by Churn

    ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/9801f4af-69e0-43d4-839c-c2fd25b20321)

## Model evaluation
#### Prepare variable
- Create dummy variable for 'PreferredLoginDevice', 'PreferredPaymentMode', 'Gender', 'PreferedOrderCat' and 'MaritalStatus' and merge to raw data.
- Create X_train, X_test, y_train, y_test by given test_size=0.40 and random_state=42
- Create X variable scaling

#### Generate model
- Classification Model: Logistic Regression, Random Forest, KNeighbors, XGBoost
- Fixed Imbalance data: None, SMOTE, Oversampling and under sampler

#### Select the optimal model
Select XGBoost model with fixing oversampling imbalance due to the high Precision, Recall and F1 score
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/c0a45450-52a2-48e6-87a6-ea717fbf591f)

## Result

#### Model evaluation

![image](https://github.com/AsmaMora/MADT8101/assets/132048257/d2617e1b-57b7-4d0b-94da-1132a6abf1ef)


#### confusion matrix

![image](https://github.com/AsmaMora/MADT8101/assets/132048257/e0e9dd8e-4dab-421e-9833-5fa6c43be04e)

#### ROC Curve

![image](https://github.com/AsmaMora/MADT8101/assets/132048257/185c1773-b869-488e-9088-3950c41ae9db)

#### Feature importance

![image](https://github.com/AsmaMora/MADT8101/assets/132048257/a899e532-d39b-4d16-9c5a-751580e52851)

