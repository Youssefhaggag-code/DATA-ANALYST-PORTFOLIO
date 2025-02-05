# 🗂️ Sales Data Analysis for zara store

---


 1️⃣ Total Sales Volume for Each Product Category
```sql
SELECT terms AS product_category, SUM(Sales_Volume) AS total_sales_volume
FROM products
GROUP BY product_category
ORDER BY total_sales_volume DESC;

 2️⃣ Product Category with the Highest Revenue

SELECT terms AS product_category, SUM(Sales_Volume * price) AS total_revenue
FROM products
GROUP BY product_category
ORDER BY total_revenue DESC
LIMIT 1;

 3️⃣ Average Price for Each Product Category

SELECT terms AS product_category, AVG(price) AS average_price
FROM products
GROUP BY product_category
ORDER BY average_price DESC;

4️⃣ Product with the Highest Sales Volume

SELECT name, terms AS product_category, Sales_Volume
FROM products
ORDER BY Sales_Volume DESC
LIMIT 1;

5️⃣ Count of Products Available in Each Category

SELECT terms AS product_category, COUNT(*) AS product_count
FROM products
GROUP BY product_category;
🛍️ Promotion and Seasonal Insights

6️⃣ Total Sales Volume for Products on Promotion (Grouped by Category)

SELECT terms AS product_category, SUM(Sales_Volume) AS promo_sales_volume
FROM products
WHERE Promotion = 'Yes'
GROUP BY product_category;

7️⃣ Product Category with the Most Seasonal Products

SELECT terms AS product_category, COUNT(*) AS seasonal_product_count
FROM products
WHERE Seasonal = 'Yes'
GROUP BY product_category
ORDER BY seasonal_product_count DESC;

8️⃣ Revenue Difference Between Seasonal and Non-Seasonal Products

SELECT Seasonal, SUM(Sales_Volume * price) AS total_revenue
FROM products
GROUP BY Seasonal;
9️⃣ Products that Are Both on Promotion and Seasonal

SELECT name, terms AS product_category
FROM products
WHERE Promotion = 'Yes' AND Seasonal = 'Yes';
💰 Price & Sales Analysis

🔟 Products with Sales Volume Above the Average of Their Category


WITH category_avg AS (
    SELECT terms, AVG(Sales_Volume) AS avg_sales
    FROM products
    GROUP BY terms
)
SELECT p.name, p.terms AS product_category, p.Sales_Volume
FROM products p
JOIN category_avg c ON p.terms = c.terms
WHERE p.Sales_Volume > c.avg_sales;



📂 Dataset Fields:
Product_ID: Unique identifier for products
Product_Position: Location in the store (Aisle, End-cap, etc.)
Promotion: Whether the product is on promotion (Yes/No)
Seasonal: Whether the product is seasonal (Yes/No)
Sales_Volume: Units sold
Name: Product name
Price: Price of the product
Currency: Pricing currency (USD)
Terms: Product category (jackets, sweaters, t-shirts, shoes, jeans)
Section: Store section (Women, MAN)
