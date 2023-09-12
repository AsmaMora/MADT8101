# Customer Segmentation
#### Definition
Customer segmentation, in simple terms, involves splitting customers into groups based on their characteristics and behavior. This enables the company to gain a deeper understanding of customer needs and create customized marketing strategies for each group, making sales efforts more effective. This focused approach enhances customer engagement, leading to increased loyalty and meaningful interactions.

#### Benefits
Customer segmentation helps companies gain deeper insights into their customers, refine marketing and sales tactics, and identify key customer segments to invest in. It also aids in improving marketing techniques and action plans.

# Product Recommendation
#### Definition
A product recommendation is basically a filtering system that seeks to predict and show the items that a user would like to purchase. It may not be entirely accurate, but if it shows you what you like then it is doing its job right.

#### Benefits
1. Provide personalized shopping experiences to customer by suggesting products based on a user's past behavior, preferences, and demographics.
2. Enhanced User experience: Recommendations make the shopping process more convenient and enjoyable, helping users find what they're looking for faster.
3. Cross-Selling and Upselling: Recommendations can suggest complementary or higher-priced items, increasing the average order value.

## Example of creating a customer segmentation and product recommendation
A distribution company which sales various health product and has 5 service locations in Asia would like to reach out to their customers more effectively by increasing personalized transactions, improve brand loyalty and customer life time value by performing.

  1. **Customer segmentation** to reach out customers more effectively
  2. **Product recommendation** to boost revenue and engagement by sending personalized message

## Dataset overview

#### 1. Sales transaction data from 2021 - 2023 (2,404,316 rows)

  **Data dictionary**
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/624fc815-f79e-4190-9eda-1032ec9dd3b9)

#### 1. Member master data (590,565 rows)

  **Data dictionery**
   ![image](https://github.com/AsmaMora/MADT8101/assets/132048257/9060bd69-1f73-44c6-abe0-038bf2f73944)

## Sanity Check

#### Sales transaction

  1. **Missing value** Total rows of the data set are 2,406,316 rows and have null value in columns total_amt, product_json, discount and paid_amt

     **Clean data:** Remove row which have null in column total, amt and product_json

  2. **Incomplete dataset** From the sales transaction tables, we found the missing data in Y2021 from M6 – M12

     **Clean data:** Exclude Y2021 for the dataset used to develop the model

  3. **Special data characteristic** There is a specially formatted column in column name product_json. The column has data in json format that includes the products and the quantity purchased for each transaction

     **Clean data:** Split the column to display 1 product per column and quantity of each product

  4. **Incorrect format** There is incorrect data format in column payment_date

     **Clean data:** Convert to date time format

  5. **Lack of essential data** No. price per product and member of each customer

     **Clean data:**

      - Product price Calculation by mathematic formula
        1. Transaction which contain one product

           Price(A) = Total amount / Qty.

        2. Transaction which contain more than one product

           Price(B) = (Total amount – (Price(A) x Qty(A)) / Qty(B)

      - Member of each customer mapping from data member

## Assumption
1. Focus on total amount by ignoring paid amount because there are only 50K members were paid more than zero from total customer around 578K members.
2. Using data from the most recent two months in 2023, recommend a product in each cluster.

## Data transformation
#### 1. Customer single view
Summarize sales transaction data to display customer single view and use to develop customer clustering model.

**Ideation**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/859597ab-5073-4407-87dc-ed56534e7d3a)

**Data dictionary**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/c8202814-1013-4bd6-aaff-958f2b7ba3a6)

**Result:** [Customer_feature.parquet](./customer_feature_2022.01.01_2023.07.parquet)
#### 2. Unpivot data product
Transform sales transaction data by unpivoting product and quantity columns of each transaction to rows.
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/887e8b82-cec7-44dc-8d4d-2a171fda9922)

**Result:** [Trans_data_unpivot.parquet](./trans_data_unpivot.parquet)
## Customer Segmentation by K-Means Clustering
Segment customer from customer single view result data

**Notebooks:** [Customer Segmentation](./MADT8101_Customer_segmentation.ipynb)

**Google colab:** [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AsmaMora/MADT8101/blob/main/4.Customer_Segmentation&Product_Recommendation/MADT8101_Customer_segmentation.ipynb)

**Feature summary**

Behaviour

* Total amount: Total spending amount per customer
* Total quantity: Total sales volume per customer
* Frequency: No. of transaction per customer
* Visit period: Period from first date to last date transaction of each customer
* Mean time between purchase: Started date - Last date then divided by frequency
* Basket size: Average price per unit per customer
* Order size: Average spending per order per customer
* Visit size: Average sales volume per order per customer
* CLTV: Customer Lifetime Values
* Discount amount: Total discount amount per customer
* Visit center: No. of visit center of each customer

Ratio

* %Qty by price range: Proportion of sales volume in any price range (4 ranges)

Distribution

* Member: No. of Member (Downline) of each customer

### Find the optimal number of clusters
Select K = 3 with silhoette score = 0.553
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/76d5fb38-d598-4e8a-961c-5656efd581b7)

### Principle Component Analysis
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/ce25bd26-008e-42e5-977c-d5739fe3b30f)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/8c8471bb-af75-4897-b040-723a4d99456a)

### Feature Importance
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/03a2444f-070f-414d-9196-fce6cec48bec)

### Summarize Custers Result
**No. of customers and total spending by cluster**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/8ac9ec05-694f-4c6a-a849-849a6ecd3296)

**Average of feature values by cluster**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/9cef5e58-8db8-449f-91fc-1e464bff41cd)

### Result conclusion
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/966a32f8-c32c-441c-b7a2-1d3b7a93f60c)


## Product Recommendation by Cosine Similarity Model
From clustering result we would like to recommend product for each group.

### Prepare data
Map cluster result to sales transaction unpivot data to separate customer into groups.
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/d05008b0-34ad-4101-8499-97e5962d2ef3)

**Result:**
[transaction_cluster0.parquet](./transaction_cluster0.parquet) , 
[transaction_cluster1.parquet](./transaction_cluster1.parquet) , 
[transaction_cluster2.parquet](./transaction_cluster2.parquet)

### Cosine Similarity Model

**Notebooks:** [Product_Recommendation](./MADT8101_Product_recommendation.ipynb)

**Google colab:** [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AsmaMora/MADT8101/blob/main/4.Customer_Segmentation&Product_Recommendation/MADT8101_Product_recommendation.ipynb)

**Method**
#### 1. Import Function
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/39da8713-9742-4888-9ff2-d7d4dc3fed3e)

#### 2. Check missing value 
There are no null value in any column.
   
#### 3. Create Member ID VS Product qty Matrix by pivot table function
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/f2713137-5451-4386-8c78-c6f1702529e3)

#### 4. Create User to User similarity matrix
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/e4901a59-1ad0-4056-b555-a1482add374f)

#### 5. Testing by random pick Member ID to display the most similar Member ID.
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/93dddd4a-1833-46d3-8149-121db5bd5789)

#### Display the list of items recommended for Y in each group
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/d4458054-2bf8-4fd1-9337-89862b8e0e43)

### Example of implementation
#### Display product recommendation to customer on e-commerce platfrom
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/0c249770-5441-45a9-83eb-2c19cabe56d2)

#### Create customer dashboard
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/792b705d-9701-45a5-ae90-732ae8494aed)



 






