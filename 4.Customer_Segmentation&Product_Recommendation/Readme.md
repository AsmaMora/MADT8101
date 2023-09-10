# Customer Segmentation
### Definition
Customer segmentation, in simple terms, involves splitting customers into groups based on their characteristics and behavior. This enables the company to gain a deeper understanding of customer needs and create customized marketing strategies for each group, making sales efforts more effective. This focused approach enhances customer engagement, leading to increased loyalty and meaningful interactions.

### Benefit
Customer segmentation helps companies gain deeper insights into their customers, refine marketing and sales tactics, and identify key customer segments to invest in. It also aids in improving marketing techniques and action plans.

# Product Recommendation
### Definition
A product recommendation is basically a filtering system that seeks to predict and show the items that a user would like to purchase. It may not be entirely accurate, but if it shows you what you like then it is doing its job right.

### Benefit

# Case study
A distribution company which sales various health product and has 5 service locations in Asia would like to reach out to their customers more effectively by increasing personalized transactions, improve brand loyalty and customer life time value by performing

  1. **Customer segmentation** to reach out customers more effectively
  2. **Product recommendation** to boost revenue and engagement by sending personalized message

**Data:**

**Notebooks:**

**Google colab:**

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

2. **Unpivot data product**

Transform sales transaction data by unpivoting product and quantity columns of each transaction to rows.
