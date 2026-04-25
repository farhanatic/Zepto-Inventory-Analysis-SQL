SELECT * FROM zepto_v2;

DESCRIBE zepto_v2;

SHOW TABLES;

SELECT COUNT(*) FROM zepto_v2;

ALTER TABLE zepto_v2 
ADD COLUMN sku_id INT NOT NULL AUTO_INCREMENT FIRST,
ADD PRIMARY KEY (sku_id);

ALTER TABLE zepto_v2 
RENAME COLUMN `ï»¿Category` TO category;

-- different product categories
SELECT DISTINCT Category FROM zepto_v2
ORDER BY Category;

-- products in stock and out of stock
SELECT outOfstock, COUNT(sku_id)
FROM zepto_v2
GROUP BY outOfStock;

-- products with price = 0
SELECT * FROM zepto_v2
WHERE mrp = 0 OR discountedSellingPrice = 0;

DELETE FROM zepto_v2
WHERE mrp = 0;

SET SQL_SAFE_UPDATES = 0;

DELETE FROM zepto_v2 
WHERE mrp = 0;

SET SQL_SAFE_UPDATES = 1;

-- convert paise to rupees
SET SQL_SAFE_UPDATES = 0;

UPDATE zepto_v2 
SET mrp = mrp / 100.0, 
    discountedSellingPrice = discountedSellingPrice / 100.0;

SET SQL_SAFE_UPDATES = 1;

SELECT mrp, discountedSellingPrice FROM zepto_v2

-- Q1. Find the top 10 best-value products based on the discount percentage.
SELECT DISTINCT name, mrp, discountPercent
FROM zepto_v2
ORDER BY discountPercent DESC
LIMIT 10;

-- Q2. What are the Products with High MRP but Out Of Stock.
SELECT DISTINCT name, mrp 
FROM zepto_v2 
WHERE outOfStock = 'True' AND mrp > 300 
ORDER BY mrp DESC;

-- Q3. Calculate Estimated Revenue for each category.
SELECT 
    category, 
    SUM(quantity * discountedSellingPrice) AS estimated_revenue
FROM zepto_v2
GROUP BY category
ORDER BY estimated_revenue DESC;

-- Q4. Find all products where MRP is greater than 500 and discount is less than 10%.
SELECT DISTINCT name, mrp, discountPercent
FROM zepto_v2
WHERE mrp > 500 AND discountPercent < 10
ORDER BY mrp DESC, discountPercent DESC;

-- Q5. Find the top 5 categories offering the highest average discount percentage.
SELECT category,
ROUND(avg(discountPercent),2) AS avg_discount
FROM zepto_v2
GROUP BY category
ORDER BY avg_discount DESC
LIMIT 5;

-- Q6. Find the price per gram of products above 100g and sort by best value.
SELECT DISTINCT name, weightInGms, discountedSellingPrice,
ROUND(discountedSellingPrice/weightInGms,2) AS price_per_gram
FROM zepto_v2
WHERE weightInGms >= 100
ORDER BY price_per_gram;

-- Q7. Group the products into cartegories like low, medium, bulk.
SELECT DISTINCT name, weightInGms,
CASE WHEN weightInGms < 1000 THEN 'Low'
     WHEN weightInGms < 5000 THEN 'Medium'
     ELSE 'Bulk'
     END AS weight_category
FROM zepto_v2;

-- Q8. What is the total inventory weight per category
SELECT category,
SUM(weightInGms * availableQuantity) AS total_weight
FROM zepto_v2
GROUP BY category
ORDER BY total_weight;