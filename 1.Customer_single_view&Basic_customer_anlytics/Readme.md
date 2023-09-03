# Customer Single View

### Definition

Customer Single view is a set of information which gather all the data about the customer for example their personal data, their sales transaction and processing into single view

Customer single view can create in a customer data platform (CDP) to centralize all user information and make it available across the related teams in the company to query and analysts

### Benefit
- Understand customer better on their profile, purchasing behavior etc. 
- Helps to make better customer relationships by providing consistent interactions across touchpoints and departments that meet the need of customer

### Example of creating a customer single view from supermarket's data

**Data:** [supermarket.parquet](./supermarket.parquet)

**Notebooks:**

**Google Colab:**

**Dataset overview**

The dataset is the sales transactions data of a supermarket from year 2006 to 2008 and the details of each columns are as per the table below.
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/22570d7d-0f02-4c24-b370-a3a343ec3f5e)


**Assumption**

The data includes member and non-memer transactions and we found the member thansaction cover 85% of overall transaction. Therefore, in this example will focus on member transaction only.

**Sanity check and clean raw data**

 1. **Check missing value** Total rows of the dataset are 578,082 rows and have null value in columns CUST_CODE, CUST_PRICE_SENSITIVITY and CUST_LIFESTAGE

    **Clean data**: Remove row which have null in column CUST_CODE to show only the members transaction.

2. **Incorrect format** There is incorrect data format in column SHOP_DATE.

   **Clean data**: Convert to date time format.

3. **Missing label column** There are no label column for clarify the value of columns CUST_PRICE_SENSITIVITY, CUST_LIFESTAGE, BASKET_SIZE.

   **Clean data**: Prepare new label columns.

**Data transformation**

After cleaning and preparing raw data, we will create new features and summarize the data to get a single customer view.
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/1a08f5fa-b31c-4184-8e7b-01fdba321f08)


**Result:** [single_view.csv](./Customer_Single_View_result.csv)

# Basic customer analytics

From the customer single view result, we will use it to segment customers into groups to analyze data, find insight, and create actions to reach each customer group more appropriately.

## K-Means Clustering

**Notebooks:**

**Google Colab:**

**Feature summary**

Behaviour

* Total_Spend: Total spending per customer code
* ARPU : Average sales volume per visit per customer
* CLTV : Customer lifetime values
* MTBP : Meantime between purchase 

Ratio
* Price sensitivity Ratio: Percentage of each price sensitivity per customer
* Basket Type Ratio: Percentage of each basket type per customer
* Mission Ratio: Percentage of each mission type per customer
* Basket Size Ratio: Percentage of each basket size percustomer

### Find the optimal number of clusters

Select K = 4 with silhoette score = 0.183
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/4bd4bc3d-4903-4f65-8fe7-76eb8bfa1f90)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/a8fc6eca-d5dd-4c43-82e4-a5462838bb24)

### Principle Component Analysis
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/5f8423ce-b3f0-4b32-a665-625e9aa48834)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/2d11f10a-f463-4821-917e-a72c7d770671)

### Feature Importance
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/695f1008-782e-4ea0-bb78-04d84bfe7b0d)

### Summarize Custers Result

**No. of customers and total spending by cluster**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/3d93df36-44a6-4caf-81b9-d7922e66e4d5)

**Average of feature values by cluster**
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/1d29bfeb-400d-4962-96c7-ecfc463dd724)

### Conclution
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/33f8571d-9236-44d1-91d9-4020387941fd)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/a1b5f409-7cd0-4c4f-91b3-9c1c03e274c2)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/48d36558-e000-45f0-ab25-c59bf169b659)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/267ba30d-d8ea-4dcc-978a-20a66bc6bdd5)
![image](https://github.com/AsmaMora/MADT8101/assets/132048257/eef812e5-3eea-4a07-bc91-a369c02a4948)
