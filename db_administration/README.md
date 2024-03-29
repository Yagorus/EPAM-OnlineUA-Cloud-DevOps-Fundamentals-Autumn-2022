# Part 1

1. Download MySQL server for your OS on VM. 

Begin by updating the package lists on your machine:

`sudo apt update`

 Install the MySQL server package using the following command:

`sudo apt install mysql-server`

 After that, start the MySQL service:

`sudo service mysql start`

 To check the status of MySQL:

`sudo service mysql status`

![status_db.png](../img/status_db.png)

2. Select a subject area and describe the database schema, (minimum 3 tables) 

![db_schema.png](../img/db_schema.png)

This schema includes a `products` table with columns for the product ID (which is the primary key and auto-increments), the name, price, and stock of each product. It also include `customers` table with columns for the customer ID (which is the primary key and auto-increments), the name, email, and phone number. and lastly it has an `orders` table with columns for the order ID (which is the primary key and auto-increments), the customer ID (which is a foreign key referencing the `customer_id` column in the `customers` table), and the order date. Note this is just a simple example, based on your requirement you may need to add/modify tables and columns accordingly.

4. Create a database on the server through the console. 

Login in mysql server with command `sudo mysql -u root -p` enter root's user password

To create DB `create database store;` and we need "select" it with following command `use store`. The use statement of MySQL helps you to select/use a database. You can also change to another database with this statement. Once you set the current database it will be same until the end of the session.

Next step it's adding tables like in schema:

For products table:
```mysql
CREATE TABLE products (
 product_id INT AUTO_INCREMENT PRIMARY KEY,
 name VARCHAR(255) NOT NULL,
 price DECIMAL(10,2) NOT NULL,
 stock INT NOT NULL
);

CREATE TABLE customers (
 customer_id INT AUTO_INCREMENT PRIMARY KEY,
 name VARCHAR(255) NOT NULL,
 email VARCHAR(255) NOT NULL,
 phone_number VARCHAR(255) NOT NULL
);

CREATE TABLE orders (
 order_id INT AUTO_INCREMENT PRIMARY KEY,
 customer_id INT NOT NULL,
 order_date DATE NOT NULL,
 FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

Check result with `show tables`

![show_tables.png](../img/show_tables.png)

And get description about tables ` desc [table name]`

![desc_customers.png](../img/desc_customers.png)

![desc_orders.png](../img/desc_orders.png)

![desc_products.png](../img/desc_products.png)

6. Fill in tables. 
   Next commands will fill in tables 
```mysql
INSERT INTO products (name, price, stock) VALUES 
    ("Apples", 0.99, 100),
    ("Bananas", 0.59, 200),
    ("Oranges", 0.89, 150);

INSERT INTO customers (name, email, phone_number) VALUES 
    ("John Smith", "johnsmith@gmail.com", "555-555-5555"),
    ("Jane Doe", "janedoe@gmail.com", "555-555-5556"),
    ("Bob Johnson", "bobjohnson@gmail.com", "555-555-5557");

INSERT INTO orders (customer_id, order_date) VALUES 
    (1, "2022-01-01"),
    (2, "2022-01-02"),
    (3, "2022-01-03");
```

Check result with command `select * from [table name]`

![select_customers.png](../img/select_customers.png)
![select_orders.png](../img/select_orders.png)
![select_products.png](../img/select_products.png)
7. Construct and execute SELECT operator with WHERE, GROUP BY and ORDER BY. 
![where_use.png](../img/where_use.png)

![order_by_check.png](../img/order_by_check.png)

added more data:

![more_data.png](../img/more_data.png)


using `group by`

![group_by_check.png](../img/group_by_check.png)

using `order by`

![order_by_check2.png](../img/order_by_check2.png)

9. Execute other different SQL queries DDL, DML, DCL. 
   
Rename table from `products` to `goods`

![rename_check.png](../img/rename_check.png)

delete element from table with `product_id=3` 

![delete_check.png](../img/delete_check.png)

create new user and grant him privileges 

![create_user.png](../img/create_user.png)


11. Make a selection from the main table DB MySQL

![db_mysql.png](../img/db_mysql.png)


## PART 2
12. Make backup of your database. 

![backup_localdb.png](../img/backup_localdb.png)

dump_file.sql
``` mysql
-- MySQL dump 10.13  Distrib 8.0.31, for Linux (x86_64)
--
-- Host: localhost    Database: store
-- ------------------------------------------------------
-- Server version       8.0.31

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!50503 SET NAMES utf8mb4 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `customers`
--

DROP TABLE IF EXISTS `customers`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `customers` (
  `customer_id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `phone_number` varchar(255) NOT NULL,
  PRIMARY KEY (`customer_id`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `customers`
--

LOCK TABLES `customers` WRITE;
/*!40000 ALTER TABLE `customers` DISABLE KEYS */;
INSERT INTO `customers` VALUES (1,'John Smith','johnsmith@gmail.com','555-555-5555'),(2,'Jane Doe','janedoe@gmail.com','555-555-5556'),(3,'Bob Johnson','bobjohnson@gmail.com','555-555-5557'),(4,'Mike Johnson','mikej@gmail.com','555-555-5558'),(5,'Samantha Smith','samanthas@gmail.com','555-555-5559'),(6,'David Williams','davidw@gmail.com','555-555-5560');
/*!40000 ALTER TABLE `customers` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `goods`
--

DROP TABLE IF EXISTS `goods`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `goods` (
  `product_id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `price` decimal(10,2) NOT NULL,
  `stock` int NOT NULL,
  PRIMARY KEY (`product_id`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `goods`
--

LOCK TABLES `goods` WRITE;
/*!40000 ALTER TABLE `goods` DISABLE KEYS */;
INSERT INTO `goods` VALUES (1,'Apples',0.99,100),(2,'Bananas',0.59,200),(4,'Bread',2.49,50),(5,'Milk',2.99,75),(6,'Eggs',2.19,90);
/*!40000 ALTER TABLE `goods` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `orders`
--

DROP TABLE IF EXISTS `orders`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `orders` (
  `order_id` int NOT NULL AUTO_INCREMENT,
  `customer_id` int NOT NULL,
  `order_date` date NOT NULL,
  PRIMARY KEY (`order_id`),
  KEY `customer_id` (`customer_id`),
  CONSTRAINT `orders_ibfk_1` FOREIGN KEY (`customer_id`) REFERENCES `customers` (`customer_id`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `orders`
--

LOCK TABLES `orders` WRITE;
/*!40000 ALTER TABLE `orders` DISABLE KEYS */;
INSERT INTO `orders` VALUES (1,1,'2022-01-01'),(2,2,'2022-01-02'),(3,3,'2022-01-03'),(7,4,'2022-01-04'),(8,5,'2022-01-05'),(9,6,'2022-01-06');
/*!40000 ALTER TABLE `orders` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2023-01-16 17:06:04
~
~
```




13. Delete the table and/or part of the data in the table. 

Delete `goods` table from `store` database:

![delete_table.png](../img/delete_table.png)

14. Restore your database. 

Restoring `goods` table and show content in it

![restore_db.png](../img/restore_db.png)
15. Transfer your local database to RDS AWS. 

First - need go to AWS web page, choose RDS section and create database. 

![create_db_aws.png](../img/create_db_aws.png)

Go to database, create there db with name `store` and use dump file:

![connect_to_rds.png](../img/connect_to_rds.png)

![transfer_localdb_to_rds.png](../img/transfer_localdb_to_rds.png)

16. Connect to your database. 

Now we can connect to db

![connection_to_db_rds.png](../img/connection_to_db_rds.png)


17. Execute SELECT operator similar step 6. 

![select_for_all_tables.png](../img/select_for_all_tables.png)

18. Create the dump of your database.

![backup_for_rds.png](../img/backup_for_rds.png)