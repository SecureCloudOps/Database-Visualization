
# Visualize a Relational Database


**Author:** Mohamed Mohamed  
**Email:** mohamed0395@gmail.com

---

## Visualise a Relational Database

![Image](https://imgur.com/4Eni1mm.png)
---

## Introducing Today's Project!

### What is Amazon RDS?

Amazon RDS (Relational Database Service) is a **managed database service** that simplifies the setup, operation, and scaling of relational databases in AWS. It supports multiple database engines like **MySQL, PostgreSQL, SQL Server, MariaDB, and Amazon Aurora**.  

RDS is useful because it **automates administrative tasks** such as backups, patching, and scaling, reducing operational overhead. It also provides **high availability, security, and performance optimization**, making it an efficient choice for running databases in the cloud.

### How I used Amazon RDS in this project

I used Amazon RDS in today’s project to **create and manage a relational database** for storing data securely. I set up an **RDS instance with MySQL**, configured security groups to **restrict access**, and connected it to **Amazon QuickSight** for data visualization. By using RDS, I was able to **store, query, and analyze data efficiently** while benefiting from **automated backups, high availability, and scalability**.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was **how crucial security configurations would be when connecting QuickSight to RDS**. Initially, I thought it would be a simple connection, but I had to carefully **adjust security groups, restrict access, and ensure the database wasn’t publicly accessible**. It was a great learning experience in **balancing security and functionality in AWS**.

### This project took me...

This project took me approximately **a few hours to complete**, including setting up **Amazon RDS, configuring security groups, connecting QuickSight, and creating visualizations**. Most of the time was spent **ensuring security best practices**, such as **restricting access and securing the database connection** while maintaining functionality.

---

## In the first part of my project...

### Creating a Relational Database

I created my relational database in AWS by using **Amazon RDS (Relational Database Service)** and following these steps:

1. **Navigated to RDS** in the AWS Management Console and selected **Databases**.
2. Clicked on **Create Database** and chose the **Easy Create** option.
3. In the **Configuration** section:
   - Set **Engine type** to **MySQL**.
   - Selected **Free tier** for the **DB instance size**.
4. Entered **QuickSightDatabase** as the **DB instance identifier**.
5. Set **admin** as the **Master username**.
6. Chose **Self-managed** under **Credentials management** and entered a secure **Master password**.
7. Saved the database credentials and clicked **Create Database**.

Once the database was successfully created, I connected to it using a MySQL client with the provided **endpoint, username, and password**.

![Image](https://imgur.com/m0qTJBy.png)

---

## Understanding Relational Databases

A relational database is a type of database that organizes data into structured tables with rows and columns. Each table (also called a relation) stores data about a specific entity, and relationships between tables are established using keys, such as primary keys and foreign keys. This structure allows for efficient data retrieval, management, and enforcement of relationships between data points. Relational databases use **SQL (Structured Query Language)** for querying and managing data. Examples of relational database management systems (RDBMS) include MySQL, PostgreSQL, SQL Server, and Oracle Database.

### MySQL vs SQL

The difference between MySQL and SQL is that **SQL (Structured Query Language)** is a standard language used to manage and manipulate relational databases, while **MySQL** is a relational database management system (RDBMS) that uses SQL to interact with databases. In simple terms, SQL is a language, and MySQL is software that implements SQL to store, retrieve, and manage data. Other RDBMS options that use SQL include PostgreSQL, SQLite, and MariaDB.

---

## Populating my RDS instance

The first thing I did was make my RDS instance public because I needed to connect to it from my local machine using **MySQL Workbench**. By default, AWS RDS instances are private and only accessible within the assigned VPC. Making the instance public allows external connections, enabling me to manage and interact with the database remotely. 

I had to update the default security group for my RDS schema because, by default, AWS restricts access to the database for security reasons. To allow **MySQL Workbench** on my local machine to connect to the RDS instance, I needed to modify the **inbound traffic rules** in the security group. I configured the security group to allow **only my IP address** to access the database. This ensures that my RDS instance remains protected while still being accessible from my local machine.

![Image](https://imgur.com/ObEd68B.png)

---

## Using MySQL Workbench

![Image](https://imgur.com/4Eni1mm.png)

To populate my database, I used **SQL INSERT statements** in **MySQL Workbench**. After creating my schema and tables, I ran queries to add sample data into each table. This data will be used for analysis and visualization in **Amazon QuickSight**.

---

## Connecting QuickSight and RDS

To connect my RDS instance to QuickSight, I:  

1. **Updated the security group** on my RDS instance to allow inbound connections from QuickSight.  
2. **Logged into Amazon QuickSight** and navigated to **Manage Data Sources**.  
3. **Added a new data source**, selecting **MySQL (or the appropriate RDS engine)**.  
4. **Entered my RDS endpoint, database name, username, and password** to establish the connection.  
5. **Validated the connection** and imported the data into QuickSight for visualization.  

This setup enables QuickSight to pull data from my RDS instance for analytics and dashboard creation.

This solution is risky because our **RDS instance is publicly available**, meaning anyone with the endpoint and credentials can attempt to access it. This makes us vulnerable to **unauthorized access, brute force attacks, and data breaches**. A better approach would be to **restrict access** by keeping the RDS instance private and allowing connections only from trusted sources, such as an EC2 instance within the same VPC or a VPN.

### A better strategy

First, I made a new security group so that **QuickSight can securely connect to my RDS instance** without making the database publicly accessible. This security group allows inbound traffic only from **QuickSight’s IP range**, ensuring that only authorized connections can access the database. This improves security by preventing unauthorized access while still enabling QuickSight to retrieve data for visualization.

Next, I connected my new security group to QuickSight by **modifying the inbound rules** of the security group attached to my RDS instance. I allowed inbound connections from **QuickSight’s IP range** on the database port (e.g., **3306 for MySQL**). This ensures that only QuickSight can access the database securely, preventing unauthorized external access while enabling data visualization.

---

## Now to secure my RDS instance

To make my RDS instance secure, I:  

1. **Disabled public access** to prevent unauthorized external connections.  
2. **Created a new security group (RDS_SecGp)** specifically for my RDS instance.  
3. **Restricted inbound rules**, allowing only QuickSight’s security group (QuickSight_SecGp) to access the database.  
4. **Used VPC settings** to ensure the database remains private and accessible only within the network.  
5. **Enabled encryption and IAM authentication** for an extra layer of security.  

These steps ensure that my RDS instance is **protected from unauthorized access** while still being accessible to QuickSight for data analysis.

I made sure that my RDS instance could be accessed from QuickSight by **modifying the security group rules**. I created a dedicated **RDS security group** and allowed inbound connections **only from QuickSight's security group**. This ensures that **QuickSight can connect to RDS** while keeping the database private and protected from unauthorized access.

![Image](https://imgur.com/0yGjW5S.png)

---

## Adding RDS as a data source for QuickSight

![Image](https://imgur.com/ItDq4Dc.png)

This data source is different from my initial data source because it is now **securely connected through a dedicated security group**, rather than being publicly accessible. The connection is restricted to authorized access from QuickSight, ensuring better security while still allowing data analysis. Additionally, the dataset may have been updated or refined for more accurate insights and visualizations.

![Image](https://imgur.com/fKnnex3.png)

---

---
