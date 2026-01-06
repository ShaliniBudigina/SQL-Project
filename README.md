# SQL-Project
-- Create Tables
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    join_date DATE
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);

CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    quantity INT,
    sale_date DATE
);

-- Insert Data
INSERT INTO customers VALUES
(1,'Ravi','Hyderabad','2023-01-10'),
(2,'Anjali','Vijayawada','2023-03-15'),
(3,'Kiran','Guntur','2023-05-20');

INSERT INTO products VALUES
(101,'Laptop','Electronics',50000),
(102,'Mobile','Electronics',20000),
(103,'Headphones','Accessories',2000);

INSERT INTO sales VALUES
(1,1,101,1,'2023-06-01'),
(2,2,102,2,'2023-06-05'),
(3,1,103,3,'2023-06-10'),
(4,3,102,1,'2023-06-12');
SELECT SUM(p.price * s.quantity) AS total_revenue
FROM sales s
JOIN products p ON s.product_id = p.product_id; # total_revenue
                                                    116000.00
SELECT c.customer_name,
       SUM(p.price * s.quantity) AS total_spent
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
JOIN products p ON s.product_id = p.product_id
GROUP BY c.customer_name; # customer_name	     total_spent
                               Ravi            	56000.00
                               Anjali	          40000.00
                               Kiran	          20000.00
SELECT p.product_name,
       SUM(s.quantity) AS total_quantity
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_quantity DESC;#  product_name	total_quantity
                                   Mobile	            3
                                   Headphones	        3
                                   Laptop	            1
  
SELECT MONTH(sale_date) AS month,
       SUM(p.price * s.quantity) AS revenue
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY MONTH(sale_date);# month    	revenue
                              6        116000.00 
                              6
