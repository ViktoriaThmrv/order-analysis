# Order-Analysis

This is a guided SQL project, based on ["Advanced SQL Retrieval Queries in SQLiteStudio" by Judy Richardson](https://www.coursera.org/projects/advanced-sql-retrieval-queries-in-sqlitestudio). The document comprises a section with 11 statements extracted from the guided project and a [section](#statements-created-by-me) with 3 statements authored by me.

## Question and answer

### The SQL queries addressing the following questions are extracted from the guided project.

#### 1. Determine the average price of orders and identify those with multiple items.

```sql
SELECT
    shipcompany,
    COUNT(ordnum) AS total_orders_shipped
FROM
    shipper
JOIN
    orders ON shipper.ShipID = orders.ShipID
GROUP BY
    shipcompany;
``` 

##### The first query calculates the average price and counts the number of items for each order "ordnum" by retrieving data from the "orderitem" table. The results are grouped by order number using the "GROUP BY" clause. Thus, it provides insights into the average price per order and identifies orders with multiple items based on the item count.

#### 2. Which shipper ships the most orders?

```sql
SELECT
    shipcompany,
    COUNT(ordnum) AS total_orders_shipped
FROM
    shipper
JOIN
    orders ON shipper.ShipID = orders.ShipID
GROUP BY
    shipcompany;
```
##### Here we analyze the shipping companies to determine which one handles the most orders. By counting the orders associated with each company "shipcompany", we retrieve data from the "shipper" and `orders` tables. Utilizing the "GROUP BY" clause, the results are grouped by shipping company, offering insights into the volume of orders each company manages.

#### 3. Count the number of products and items on each order.

```sql
SELECT
    ordnum,
    COUNT(prodid) AS total_products_ordered
FROM
    orderitem
GROUP BY
    ordnum;
```
##### To explore the details of each order, we analyze the quantity of products and items they contain. By selecting the order number "ordnum" and counting the associated products "count(prodid)", we gather insights from the 'orderitem" table. Grouping the results by order number with the "GROUP BY" clause allows us to discern the product and item counts for each order.

#### 4. List only the orders that have more than 1 product.

```sql
SELECT
    ordnum,
    COUNT(prodid) AS total_products
FROM
    orderitem
GROUP BY
    ordnum
HAVING
    COUNT(prodid) > 1;
```
##### To narrow down our focus to orders that contain multiple products, we use this query to sift through the orders and identify those with more than one product listed. By selecting the order number "ordnum" and counting the associated products "count(prodid)", we can examine the composition of each order in the `orderitem` table. Then, using the "HAVING" clause with the condition "count(prodid) > 1", we filter the results to isolate orders that meet this criterion.

#### 5. Find orders that have more than 1 order from Minessota.

```sql
SELECT
    ordnum,
    COUNT(orderitem.prodid) AS product_count
FROM
    orderitem
JOIN
    product ON orderitem.prodid = product.prodID
JOIN
    fabric ON product.prodfabcode = fabric.fabcode
JOIN
    supplier ON fabric.fabsupplier = supplier.supID
WHERE
    supplier.supstate = 'MN'
GROUP BY
    ordnum
HAVING
    COUNT(orderitem.prodid) > 1;
```
##### In this query, we're searching for orders with multiple items that originate from Minnesota-based suppliers. By joining several tables like "orderitem", "product", "fabric", and "supplier", we first link the order items to their corresponding products and then to their suppliers. The condition "supstate = 'MN'" ensures that we only include orders from Minnesota suppliers. Finally, using the "GROUP BY" clause alongside "HAVING COUNT(orderitem.prodid) > 1", we filter the results to only display orders with more than one item, as requested.

#### 6. Display a list of products that have prices higher than the average product price.

```sql
SELECT
    proddesc,
    prodprice
FROM
    product
WHERE
    prodprice > (
        SELECT
            AVG(prodprice)
        FROM
            product
    );
```
##### This query retrieves product descriptions and prices from the "product" table, filtering only those products whose prices exceed the average price of all products. It achieves this by utilizing a subquery "(SELECT AVG(prodprice) FROM product)" to calculate the average product price and then comparing each product's price against this average using the "WHERE" clause.

#### 7. Query the first and last names of customers who placed an order on Dec 14 2020.

```sql
SELECT
    custlastname,
    custfirstname
FROM
    customer
WHERE
    custid IN (
        SELECT
            ordcustid
        FROM
            orders
        WHERE
            orddate = '2020/12/14'
    );
```
##### Now, to explore how to extract the first and last names of customers who made purchases on December 14, 2020, we use this query, which focuses on filtering customer records from the "customer" table, specifically targeting those whose IDs are linked to orders placed on that particular date. By doing so, we can identify the customers who participated in transactions on December 14th, 2020.

#### 8. Calculate the profit.

```sql
SELECT
    proddesc,
    prodprice,
    prodcost,
    prodprice - prodcost AS Profit
FROM
    product;
```
##### For this SQL query, we're looking at the financial performance of each product. By subtracting the production cost from the selling price, we find out the profit margin for each item. The query presents the product description, selling price, production cost, and the resulting profit, offering a comprehensive insight into the financial viability of our product inventory.

#### 9. Produce the amount due on each order.

```sql
SELECT
    ordnum,
    prodid,
    quantity,
    price,
    (quantity * price) AS amtDue
FROM
    orderitem;
```
##### This SQL statement computes the total amount owed for each item within an order. By multiplying the quantity of each product by its respective price, it derives the individual amount due. The query presents details such as order number, product ID, quantity, price, and the resulting amount owed, offering a comprehensive financial breakdown for each order.

#### 10. Calculate the total due for the entire order.

```sql
SELECT
    ordnum,
    SUM(quantity * price) AS amtDue
FROM
    orderitem
GROUP BY
    ordnum;
```
##### This query calculates the total amount due for each order by summing up the product of quantity and price for all items in each order. It selects the order number "ordnum" and applies the "SUM" function to compute the total amount due, which is aliased as "amtDue". By grouping the results by order number, it provides a concise overview of the total due amount for each order in the dataset.

#### 11. Calculate the amount due for each of the items on the orers along with the discount.

```sql
SELECT
    ordnum,
    prodid,
    discountlevel,
    (quantity * price) AS amtDue,
    CASE discountlevel
        WHEN 'b' THEN (quantity * price) * 0.95
        WHEN 'c' THEN (quantity * price) * 0.90
        WHEN 'd' THEN (quantity * price) * 0.80
        ELSE (quantity * price)
    END AS DueAfterDiscount
FROM
    orderitem;
```
##### For this statement, we're computing the amount due for each item on orders, taking into account any applicable discounts. We're selecting the order number, product ID, discount level, original amount due, and then utilizing a CASE statement to adjust the amount due based on the discount level ("b", "c", or "d"). This allows us to derive the final amount due after applying the relevant discount for each item on the orders.

<a name="statements-created-by-me"></a>
## This section includes statements created by me. These questions were generated using ChatGPT, and I wrote the code, utilizing the database referenced at the beginning of this repository.

#### 1. Which products have the highest sales volume?

```sql
SELECT 
    p.prodID,
    p.prodDesc,
    SUM(oi.Quantity) AS TotalSalesVolume
FROM 
    orderitem oi
JOIN 
    Product p ON oi.ProdID = p.prodID
GROUP BY 
    p.prodID, p.prodDesc
ORDER BY 
    TotalSalesVolume DESC;
```

##### In this query, we're examining the sales performance of products by calculating the total quantity sold for each item. By combining data from the order item and product tables and using the SUM function to aggregate quantities, we determine the overall sales volume for each product. Finally, the results are sorted in descending order based on sales volume, highlighting the products with the highest sales.

#### 2. Which fabric color is the most popular among customers?

```sql
SELECT 
    f.FabColor,
    SUM(oi.Quantity) AS TotalQuantityOrdered
FROM 
    orderitem oi
JOIN 
    Product p ON oi.ProdID = p.prodID
JOIN 
    fabric f ON p.prodFabCode = f.FabCode
GROUP BY 
    f.FabColor
ORDER BY 
    TotalQuantityOrdered DESC
LIMIT 1;
```

##### In this statement, we're exploring which fabric color attracts the most attention from customers. By combining data from the order item, product, and fabric tables and aggregating the quantities ordered for each fabric color using the SUM function, we gain insights into customer preferences. The results are then sorted in descending order based on the total quantity ordered, revealing the fabric color that garners the highest interest from customers.

#### 3. Which customers have taken advantage of the highest discount levels?

```sql
SELECT 
    Customer.CustID,
    Customer.CustLastName,
    Customer.CustFirstName,
    SUM(CASE WHEN orderitem.DiscountLevel = 'b' THEN orderitem.Price * orderitem.Quantity * 0.05
             WHEN orderitem.DiscountLevel = 'c' THEN orderitem.Price * orderitem.Quantity * 0.10
             WHEN orderitem.DiscountLevel = 'd' THEN orderitem.Price * orderitem.Quantity * 0.20
             ELSE 0 END) AS TotalDiscountAmount
FROM 
    Customer
JOIN 
    Orders ON Customer.CustID = Orders.OrdCustID
JOIN 
    orderitem ON Orders.OrdNum = orderitem.OrdNum
GROUP BY 
    Customer.CustID,
    Customer.CustLastName,
    Customer.CustFirstName
ORDER BY 
    TotalDiscountAmount DESC;
```

##### Finally, for this query, we're identifying customers who have benefited the most from various discount levels. By joining data from the Customer, Orders, and orderitem tables and using conditional logic within a SUM function, we calculate the total discount amount for each customer based on their order items' discount levels (in this scenario, the discounts are 0.50%, 20% and 50%). The results are then grouped by customer ID, last name, and first name, providing a breakdown of the total discount amount each customer has received, sorted in descending order to highlight those who have taken advantage of the highest discount levels.
