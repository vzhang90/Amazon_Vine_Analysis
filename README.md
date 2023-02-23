# Amazon Vine Analysis
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. This project analyzes Amazon reviews written by members of the paid Amazon Vine Program to determine whether there is bias in Vine reviews when paid vs unpaid.

## Results
***Vine Table DataFrame categorizing paid vs unpaid types of reviews***
![vine table bias](https://github.com/vzhang90/Amazon_Vine_Analysis/blob/main/Images/Vine_table_paid_vs_unpaid.png)  
- 261 Vine reviews vs 24,040 non-Vine reviews
- 106 Vine reviews were 5 stars while 10,899 non-Vine reviews were 5 stars
- 40.61% of Vine reviews were 5-star while 45.337% of non-Vine reviews were 5-star

## Summary 
Because the overall percentage of 5-star reviews was proportionally lower in paid Vine reviews vs unpaid non-Vine reviews, there does not seem to be positivity bias. Further investigations could look at the opposite aspect of negativity bias by running same analysis on 1-star reviews to determine if there is any significant bias between different types of reviews.