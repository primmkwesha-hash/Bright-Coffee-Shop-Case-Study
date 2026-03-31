
--1. Run the entire table
Select * 
From `workspace`.`browns`.`bright_coffee_shop`;

--2. Checking the date range
Select 
      min(transaction_date) As min_date,
      max(transaction_date) As max_date
From `workspace`.`browns`.`bright_coffee_shop`;

--3. Checking the different store locations
Select Distinct store_location
From `workspace`.`browns`.`bright_coffee_shop`;

--4. Checking the names of different stores
Select Distinct store_location As store_name
From `workspace`.`browns`.`bright_coffee_shop`
Group By store_name;

--5 Checking products sold at our stores
 Select Distinct product_type As product_sold
 From `workspace`.`browns`.`bright_coffee_shop`
 Group By product_sold;      

--6 Checking price for each product
Select Distinct product_category, 
                product_type, 
                unit_price As product_price
From `workspace`.`browns`.`bright_coffee_shop`;

--7. Checking the lowest and highest product prices
Select Min(unit_price) As lowest_price
From `workspace`.`browns`.`bright_coffee_shop`;

Select Max(unit_price) As highest_price
From `workspace`.`browns`.`bright_coffee_shop`;

--8. Checking for NULLS in various columns
Select*
From `workspace`.`browns`.`bright_coffee_shop`
Where unit_price IS NULL
OR transaction_qty IS NULL
OR transaction_date IS NULL;

--9. Checking the day and month names
Select transaction_date,
Dayname(transaction_date) As day_name,
Monthname(transaction_date) As month_name
From `workspace`.`browns`.`bright_coffee_shop`;

--10. Checking the number of transactions per day
Select transaction_date, Count(transaction_date) As daily_transactions
From `workspace`.`browns`.`bright_coffee_shop`
Group By transaction_date;

--11. Checking the Renevue
Select unit_price,
      transaction_qty,
      unit_price * transaction_qty As revenue
From `workspace`.`browns`.`bright_coffee_shop`;


--Applying multiple functions to generate a polished dataset
Select *,
--Adding columns to enhance the table for better insights

      Dayname(transaction_date) As Day_name,
      Monthname(transaction_date) As Month_name,
      Dayofmonth(transaction_date) As Date_of_month,
      
Case
      When Dayname(transaction_date) = 'Saturday' Then 'Weekend'
      When Dayname(transaction_date) = 'Sunday' Then 'Weekend'
      Else 'Weekday'
      End As Day_Classification,
--Time buckets
Case 
      When date_format(transaction_time, 'HH:mm:ss') Between '05:00:00' And '08:59:59' Then '01.Rush Hour'
      When date_format(transaction_time, 'HH:mm:ss') Between '09:00:00' And '11:59:59' Then '02.Mid Morning'
      When date_format(transaction_time, 'HH:mm:ss') Between '12:00:00' And '15:59:59' Then '03.Afternoon'
      When date_format(transaction_time, 'HH:mm:ss') Between '16:00:00' And '18:00:00' Then '04.Rush Hour'
      Else '05.Night'
      End As Time_Classification,
--Spend buckets
Case 
      When (unit_price * transaction_qty) <= 50 Then '01.Low Spend'
      When (unit_price * transaction_qty) Between 51 And 200 Then '02.Medium Spend'
      When (unit_price * transaction_qty) Between 201 And 300 Then '03.Moreki'
      Else '04.Blesser'
      End As Spend_buckets,
--Revenue
      unit_price * transaction_qty As Revenue
From `workspace`.`browns`.`bright_coffee_shop`;





