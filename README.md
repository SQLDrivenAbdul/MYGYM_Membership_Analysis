# MYGYM_Membership_Analysis 🏋️

## Project Overview

<p align="justify">
This project analyses the data of MYGYM, a fast-growing fitness center chain with multiple locations across California. MyGym offers a wide range of membership tiers, subscription models, and amenities, including group classes, personal training, and multi-location access. The goal as a Data Analyst at MYGYM is to help use membership data to uncover insights on how members engage with these services which will help in optimizing operations and designing  a well-targeted and effective membership offers.
</p>



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



``` sql
CREATE VIEW Gymnalytics 
AS (SELECT 
    member_id,
    membership_type,
    age,
    visit_per_week,
    days_per_week,
    attend_group_lesson,
    avg_time_check_in,
    avg_time_check_out,
    uses_sauna,
    duration_in_gym_minutes,
    has_drink_subscription,
    personal_training,
    self_identified_gender,
    subscription_price,
    subscription_model,
    adjusted_price,
    discount_type,
    discount_rate,
    final_price,
    access_hours,
    home_gym_location,
    latitude,
    longitude,
    join_date,
    last_visit_date,
    personal_training_hours,
    multi_location_access
FROM 
    MyGym_Fitness
)
```
&nbsp;


I created a view to select columns needed for the analysis.




### Context
Understanding customer churn is critical for any business. Although losing customers is inevitable, identifying and analyzing the root causes enables organizations to make informed, strategic decisions that could improve retention and long-term growth. For a fitness company like MyGym,where consistency of customers is key to achieving their goal of a smart and healthy body,I created a benchmark,considering members who has  been out of the gym for more than 30 days a churned customer.

![Gym Profit and Churn](churn%rate.PNG)


### Profitability and Churn By Membership type

``` sql
WITH cte 
AS(SELECT 
    membership_type,
    member_id,
    join_date,
    last_visit_date,
    final_price,
    DATEDIFF(DAY,last_visit_date,(SELECT MAX(last_visit_date) FROM Gymnalytics)) AS date_count
FROM Gymnalytics
)
,
aggregation 
AS(SELECT 
    membership_type,
    COUNT(CASE WHEN date_count > 30 THEN 1 END) AS n_churned_members,
    COUNT(member_id) AS n_existing_members,
    SUM(final_price) AS revenue_per_type
FROM cte
GROUP BY membership_type
)

SELECT 
    membership_type,
    n_churned_members,
    n_existing_members,
    revenue_per_type /(SELECT SUM(final_price) FROM Gymnalytics) * 100 AS percent_of_total_revenue 
FROM aggregation
```

### Query Output
![Gym Profit and Churn](gym_profit%20and%20churn.PNG)



