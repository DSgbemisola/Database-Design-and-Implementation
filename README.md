# Cofee Shop Database-Design-and-Implementation
This is a project on Database Design and Implementation. In this project I demostrate skills in designing a database using an ERD tool and implement the database schema using PostgreSQL and MySQL.

# Project Scenario
In this project scenario, I have recently been hired as a Data Engineer by a New York-based coffee shop chain looking to expand nationally by opening several franchise locations. They want to streamline operations and revamp their data infrastructure as part of their expansion process.

My job is to design their relational database systems for improved operational efficiencies and make it easier for their executives to make data-driven decisions.

Currently, their data resides in several systems: accounting software, supplier databases, point of sales (POS) systems, and even spreadsheets. I will review the data in all of these systems and design a central database to house all of the data. I will then create the database objects and load them with source data. Finally, I will create subsets of data our business partners require, export them, and load them into staging databases using several PostgreSQL and MySQL.

# Software used in this project
In this project, I used PostgreSQL Database and MySQL. These are all relational database management systems (RDBMS) designed to store, manipulate, and retrieve the data efficiently.

![image](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/540aee03-b250-45b4-9ef8-b38b51a08e04)

# Data used in this project
In this project, I worked with a subset of data from the Coffee shop sample data, however, I used a modified version of the data for the project, 

In this project scenario, I worked with data from the following sources:
1. Staff information held in a spreadsheet at headquarters (HQ)
2. Sales outlet information held in a spreadsheet at HQ
3. Sales data output as a CSV file from the POS system in the sales outlets
4. Customer data output as a CSV file from a custom customer relationship management system
5. Product information maintained in a spreadsheet exported from your supplier's database

# Objectives
The objectives of this project are to:
1. Identify entities
2. Identity attributes
3. Create an entity relationship diagram (ERD) using the pgAdmin ERD tool
4. Normalize tables
5. Define keys and relationships
6. Create database objects by generating and running the SQL script from the ERD tool
7. Create a view and export the data
8. Create a materialized view and export the data
9. Import data into a MySQL database using phpMyAdmin GUI tool

# Project Phases
This project was conducted in Ten (10) distinct phases as detailed below:

# Phase 1: Identifying entities
The first phase of the project was to review any existing data and identify the entities for our new system.

The following image shows sample data from each source we are working with to design our new central database. 
1. I reviewed the image and identified the entities I plan to create. See the screenshot below:
![image](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/afee7268-9c24-4e28-8e63-6bfb5eec77df)

2. I made a list of the entities I have identified. See the screenshot below:
![Task1](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/1253dc25-93df-494d-bc66-aa93ba0153df)

# Phase 2: Identifying attributes

In this second phase, I identified the attributes of all the entities I plan to create. See the screenshot below:
![Task1](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/d449dcc8-ed03-4682-b817-e97baf634e50)

# Phase 3: Creating an ERD
Now that I have defined some of our attributes and entities, I went further to determine the tables and columns for them by creating an entity-relationship diagram (ERD) in PgAdmin.
- I launched the PgAdmin on my local computer, Created a new database named COFFEE, viewed the schemas in the new COFFEE database, and then started a new ERD project using the information in the list of entities and attriutes I created in Phase 1 & 2. See screenshot below:
![image](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/58e73774-72a2-4ff7-a5a2-cda0c8d3e092)

# Phase 4: Normalizing tables
When reviewing your ERD, I noticed it does not conform to the second normal form. In this phase, I tried to normalize some of the tables within the database.

1. I reviewed the data in the sales transaction table, noting that the transaction id column does not contain unique values because some transactions include multiple products.
2. I determined which columns should be stored in a separate table to remove the repeating rows and to put this table into second normal form.
3. I added a new table named "sales_detail" to the ERD, defined the columns in the new table, and deleted the moved columns from the sales transaction table, leaving a matching column in each of the two tables to create a relationship between them later.
4. Similarly, I reviewed the data in the product table, noting that the product category and product type columns contain redundant data.
5. I determined which columns should be stored in a separate table to reduce redundant data and to put this table into a second normal form.
6. I added a new table named product_type to the ERD, defined the columns in the new table, and deleted the moved columns from the product table, leaving a matching column in each of the two tables to create a relationship between them later.

# Phase 5: Defining keys and relationships
After normalizing our tables, I defined their primary keys and relationships between the tables in our ERD.

I identified an appropriate column in each table to be a primary key and created the primary keys in the tables in our entity-relationship diagram (ERD).
See the screenshot of our ERD:
![ERD](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/59bdc44a-5e64-4d5f-9b75-cfc89750f108)

# Phase 6: Creating database objects by generating and running the SQL script from the ERD tool
After completing the ERD design, I generated an SQL script from your ERD, which I used to create our database schema. Finally, I loaded the existing data from various sources into our new database schema with the code below.

1. I downloaded the GeneratedScript.sql using: https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/CoffeeData/GeneratedScript.sql
In pgAdmin, I opened the query tool, uploaded and opened the GeneratedScript.sql file from my local computer, and then ran the script to create the tables defined in the ERD. I verified that the tables exist in the COFFEE database\’s public schema.

2. I downloaded the CoffeeData.sql using: https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/CoffeeData/CoffeeData.sql
In pgAdmin, I opened another instance of the Query tool, uploaded and opened the CoffeeData.sql file from your local computer, and then ran the script to populate the tables you just created.

See the screenshot showing the tree-view pane on the left side of the page:
![Tables](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/9655794c-ddee-4fc7-bff4-6eaef6276825)

# Phase 7: Creating a view and exporting the data
The external payroll company has requested a list of employees and the locations at which they work. The specifically requested that the list should not include the CEO or CFO who owns the company. In this phase, I created a view in our PostgreSQL database that returns this information and export the results to a CSV file.

1. In our COFFEE database, I created a new view named staff_locations_view using the following SQL:

SELECT staff.staff_id,
staff.first_name,
staff.last_name,
staff.location
FROM staff
WHERE "position" NOT IN ('CEO', 'CFO');

2. Viewed all the rows returned from the view.
3. Saved the results set to a file named "staff_locations_view.csv" on my local computer.

See the screenshot here: 
![Task7](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/31734ac7-e7e2-42a3-bb4b-06cef076a140)

# Phase 8: Creating a materialized view and exporting the data
A marketing consultant requires access to our product data in their MySQL database for a marketing campaign. Here are the steps I took to achieve this task.

I Created a materialized view in our PostgreSQL database that returns this information and exported the results to a CSV file. 

1. In our COFFEE database, I created a new materialized view named product_info_m-view using the following SQL:

SELECT product.product_name, product.description, product_type.product_category
FROM product
JOIN product_type
ON product.product_type_id = product_type.product_type_id;

2. Refreshed the materialized view with data.
3. Viewed all the rows returned from the view.
4. Saved the results set to a file named "product_info_m-view.csv" on my local computer.

See the screenshot of the view showing the tree-view pane on the left side of the page with the results in the Data Output pane:
![Task8](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/8cc56dbf-81ec-433c-b977-4112362d6247)

# Phase 9: Importing staff_location data into a MySQL database
The external payroll company has asked us to upload the staff location information to their MySQL database. Here are the steps I took to achieve this task. I:
I. launched a MySQL instance in the Cloud IDE.
2. Opened phpMyAdmin in a new tab in my browser.
3. In phpMyAdmin, I created a new database named "STAFF_LOCATIONS", then imported the location information saved in the staff_locations_view.csv file I exported from the view I created in Phase 7.
4. Explored the new table and then viewed the data in it.

See the screenshot of the contents of the new table in phpMyAdmin:
![Task9](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/e0dff4e6-41c7-4127-a9d1-0c607e6a0ab8)

# Phase 10: Import coffee_shop_products data into a MySQL database
The marketing consultant has asked us to upload the product information to their MySQL database.Here are the steps I took to achieve this task.

In phpMyAdmin, I created a new database named "coffee_shop_products", and then imported the product information saved in the product_info_m-view.csv file from our materialized view into a new table in the coffee_shop_products database.

I browsed the contents of the new table.

See the screenshot of the contents of the new table:
![Task10](https://github.com/DSgbemisola/Database-Design-and-Implementation/assets/116846702/8a18c214-9c95-4961-9292-53e829fc3fb9)





