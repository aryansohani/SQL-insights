# SQL-insights
Retail Sales SQL Analysis: A collection of SQL queries for data cleaning, exploration, and analysis on a retail sales dataset. The project includes tasks like handling NULL values, calculating total sales, analyzing customer behavior, and generating insights on product categories and sales performance.
## Questions and Answers

### Q1:write all the column for sales made on '2022-11-05'
```sql
    select * from retail_sales
    where sale_date='2022-11-05'
```
### Q2:to get category clothing with quantity =4 and in month of nov
```sql
      SELECT * 
      FROM retail_sales 
      WHERE
      category = 'Clothing'
       and
       to_char(sale_date,	'YYYY-MM')='2022-11'
       AND
       quantiy=4

```
### Q3:to select total sales for each category
```sql
     select category,
     sum(total_sale) ,
     count(total_sale)
     as total from retail_sales
     group by 1
```
### Q4:To find avg of age of people who purchased item from beaty 
```sql
     select category,
     round(avg(age),2) as mean_age from retail_sales
     where category='Beauty'
     group by 1
```
### Q5:write sql query to find all transaction where total sales is greater than 1000
```sql
     select * from retail_sales
     where total_sale >= 1000 
```
### Q6:write a sql query to find number of tarnsaction made by each gender of category
```sql
     select  
     gender , 
     count(transactions_id) as tid
     from retail_sales
     group by 1
```
### Q7: avg sale for each month and best selling month in each year
```sql
     SELECT* from
     (select 
     EXTRACT(YEAR FROM sale_date) as year,
     EXTRACT(MONTH FROM sale_date) as month,
     avg(total_sale) ,
     RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date)ORDER BY AVG(total_sale) DESC)
     from retail_sales
     group by 1,2) AS T1
     WHERE rank=1
```
### Q8: top 5 customer based on highest sales data
```sql
     select 
     customer_id,
     sum(total_sale) 
     FROM retail_sales
     group by 1
     order by 2 desc
     limit 5
```
### Q9: unqiue customer to purchase item from each category
```sql
     select count(distinct customer_id),
     category from retail_sales
     group by category
```
### Q10:write sql query to create a each shift (morning<=12,afternoon between 12,17, evening >17)
```sql
     select *,
     CASE
     when EXTRACT(HOUR FROM sale_time)<12 then 'morning'
     when EXTRACT(HOUR FROM sale_time) between 12 and 17 then 'afternoon'
     else 'evening'
     end as shift
     from retail_sales 
```
# Retail Sales SQL Analysis Project

## Conclusion

This project demonstrates the ability to clean, explore, and analyze retail sales data using SQL. The queries provided serve as a guide for tackling common data challenges, such as handling missing values, performing aggregation, and deriving insights from large datasets. By analyzing different aspects of the sales data—such as total sales, product categories, customer demographics, and time-based sales patterns—this project provides valuable insights that can help improve business decisions and strategies.

The project successfully uses SQL techniques to extract key metrics, find trends, and prepare data for further analysis. It can be easily adapted for different datasets and expanded to include more complex analyses.

## Features

- **Data Cleaning**: Identifies and removes NULL values in key columns.
- **Data Exploration**: Counts total sales records, unique customers, and distinct categories.
- **Aggregated Sales Analysis**: Calculates total sales for each category, and averages customer age for product categories.
- **Time-based Analysis**: Calculates monthly sales averages, identifies best-selling months, and categorizes sales by shifts (morning, afternoon, evening).
- **Customer and Product Insights**: Identifies top customers, analyzes purchases across categories, and tracks transaction data based on gender and other parameters.
- **Shift Classification**: Classifies sales transactions into morning, afternoon, or evening shifts based on sale time.

## Author

**Aryan Sohani**

This project was created and developed by Aryan Sohani, who is passionate about data analysis and SQL. The project demonstrates proficiency in SQL, focusing on practical applications such as data cleaning, aggregation, and trend analysis.

