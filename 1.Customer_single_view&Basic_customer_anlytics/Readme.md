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
![Dataset_Details](./Supermarket_dataset_detail.png)

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
