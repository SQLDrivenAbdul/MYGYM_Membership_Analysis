# MYGYM_Membership_Analysis 🏋️

## Project Overview
This project analyses the data of MYGYM, a fast-growing fitness center chain with multiple locations across California. MyGym offers a wide range of membership tiers, subscription models, and amenities, including group classes, personal training, and multi-location access. The goal as a Data Analyst at MYGYM is to help use membership data to uncover insights on how members engage with these services which will help in optimizing operations and designing  a well-targeted and effective membership offers.


## Data Sources
The data was gotten from Onyx Analytics monthly challenge for August. It has 25 fields of both facts and dimensional values and 1998 records.

## Tools
- Excel: Data normalization
- SQL: Data cleaning,manipulation and analysis

## Exploratory Data Analysis(EDA)
- Understand which member segments bring the most value
- Identify areas for pricing, subscription, or service optimization
- Improve customer experience through data-driven insights
- Optimize staffing and facility allocation across locations
- Explore trends in retention, usage, and upgrade behavior

## Analysis
-- Profitability
```sql
SELECT ISNULL(membership_type,'Total') AS membership_type,
	   COUNT(member_id) AS members,
	   SUM(final_price) revenue
FROM MyGym_Fitness
GROUP BY ROLLUP(membership_type)
ORDER BY revenue
```
### Query result

<img width="274" height="146" alt="gym profit" src="https://github.com/user-attachments/assets/4af58270-64f8-4a9b-bde4-d44df27fd6eb" />

A deep dive into which segment of the customers/members generates the most income reveals that the Premium membership type with 812 (40% customers) generates the most revenue with a value of 34480.86 USD, followed by Standard type with 593 (29.7% customers) generated a value of 15450.11 USD while the elite and basic are at the rare with 12155.39 and 6788.55 USD respectively.




