# Amazon Vine Analysis
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. This project analyzes Amazon reviews written by members of the paid Amazon Vine Program to determine whether there is bias in Vine reviews when paid vs unpaid.

## **Overview of Analysis**
From the following [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), the product reviews from the [US home entertainment dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Home_Entertainment_v1_00.tsv.gz) was chosen to analyze.

To perform **ETL** on these Amazon Product Reviews, a new database must first be created with **AWS RDS console** according to the following connection & security settings:
  - ***Inbound rules*** edited to add type `PostgresSQL` with the source set to `Anywhere-IPv4` 
  - ***Outbound rules*** check that the Custom Destination has `0.0.0.0/0` 
    
---      
Then to create a new database in this ***Amazon RDS server*** through **pgAdmin**, the server must be added accordingly:
  - Port Number 5432
  - Host name/address in connection settings is the URL endpoint of the previously created AWS RDS instance   

In **pgAdmin**, a new query was ran to create the following tables from this new database: `customers_table`,  `products_table`,  `review_id_table`,  `vine_table`

---
Using **Google Colab Notebook**, four DataFrames were created in [Amazon_Reviews_ETL.ipynb](https://github.com/vzhang90/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb) through **PySpark**. Once generated through **PySpark**, the DataFrames must be uploaded into **pgAdmin** in a manner/syntax that must correspond to the tables in **pgAdmin**.  
  
From **pgAdmin**, the `vine_table` is exported as [vine_table.csv](https://raw.githubusercontent.com/vzhang90/Amazon_Vine_Analysis/main/vine_table.csv).   

---

Using **Pandas** as seen in [Vine_Review_Analysis.ipynb](https://github.com/vzhang90/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb), the [vine_table.csv file](https://raw.githubusercontent.com/vzhang90/Amazon_Vine_Analysis/main/vine_table.csv) is read into DataFrame to perform further analysis.
1. The data is filtered to create a DataFrame whoch retrieves all rows where the total_votes count is equal to or greater than 20 <sub>(to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on)</sub>
2. Additionally filtered to create a DataFrame where the percentage of helpful_votes is equal to or greater than 50% 
3. The data is filtered into a DataFrame where reviews were written as part of the Vine program (paid), `vine == 'Y'`
4. Repeat Step 3, but this time retrieve all the rows where there isn't a Vine review (unpaid), `vine == 'N'`

***This analysis will help <strong>Determine the Bias of Vine Reviews</strong> by illustrating the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid)***


## Results
> **Vine Table DataFrame categorizing paid vs unpaid types of reviews**
> ![vine table bias](https://github.com/vzhang90/Amazon_Vine_Analysis/blob/main/Images/Vine_table_paid_vs_unpaid.png)  
- There were in total: 261 Vine reviews & 24,040 non-Vine reviews 
- Out of 261 total Vine reviews, 106 were 5 stars; while out of 24,040 non-Vine reviews, 10,899 were 5 stars
- 40.61% of Vine reviews were 5-star while 45.337% of non-Vine reviews were 5-star

## Summary 
Because the overall percentage of 5-star reviews was proportionally lower in paid Vine reviews vs unpaid non-Vine reviews, there does not seem to be positivity bias. Further investigations could look at the opposite aspect of negativity bias by running same analysis on 1-star reviews to determine if there is any significant bias between different types of reviews.