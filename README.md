# Fall-2021-Data-Science-Internship

This repository contains answers to all Data Science internship challenge questions from Shopify. Also, it contains a Python file with to show how I understood the dataset.

Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 


Method: Using Median instead of Mean

a.	Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

Answer: The two shops with shop_ids 42 and 78 made the data skewed i.e., shop with id 42 had a maximum of 2000 items being sold at a price of 704000 and shop 78 had a huge price per item 25725 which is a large variation comparing price of the items other shops sold. The scatter plot shows that the order values for these two shops are outliers.  Looking through the data, it has skewness. Removing outliers might not be an optimal choice if outliers also have importance. 

b.	What metric would you report for this dataset?
Answer: Using median represents behavior of 50% of the data(the middle area) which by default ignores extreme values that cause skewness in the data.

c.	What is its value?
Answer: Median obtained 284


Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

a.	How many orders were shipped by Speedy Express in total?

SELECT Shippers.ShipperName, count(Orders.OrderID) AS "Total_orders_shipped" 
FROM [Orders] LEFT join [Shippers] ON Orders.ShipperID= Shippers.ShipperID
where Shippers.ShipperName="Speedy Express"
GROUP BY Shippers.ShipperName

Result: 54

b.	What is the last name of the employee with the most orders?

SELECT e.LastName, count(o.OrderID) AS Total_Order_Count FROM Orders o LEFT JOIN Employees e
ON o.EmployeeID=e.EmployeeID
group by o.EmployeeID
order by count(o.OrderID) desc
limit 1

Result: Peacock

c.	What product was ordered the most by customers in Germany?

SELECT p.productname, od.quantity from
orderdetails od INNER JOIN  products p
on od.productid = p.productid
where od.orderid=(select o.orderid from orders o inner join customers c on o.customerid=c.customerid where c.country='Germany')
order by od.quantity desc limit 1

Result: Gorgonzola Telino

