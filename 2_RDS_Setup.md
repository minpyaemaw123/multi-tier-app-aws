# Resource Creation

## Create RDS (MySQL)


1. Create DB Subnet Groups
   
   Name: **rds-sub-grp**
   
   VPC: Default VPC
   
   ![](imgs/rds-sub-grp.png)
   
2. Create Parameter Groups

   Name: rds-para-group

   ![](imgs/rds-para-grp.png)
   
3. Create Database

   We will use **Standard Create** and choose **MySQL**

   ![](imgs/create-db-1.png)
   
   Input **Master username** and **Master password** for future use.
   
   ![](imgs/create-db-2.png)
   
   GP SSD (GP2) is used.
   
   ![](imgs/create-db-3.png)
   In DB Subnet Group, please select the subnet group **rds-sub-grp** created in step 1
   
   Security Group: backend-sg
   
   ![](imgs/create-db-4.png)
   
   Please note the Database Port **3306**, which is used in the source code for connection with the database.
   
   ![](imgs/create-db-5.png)
   
   Tick **Enable Enhanced Monitoring**
   
   For **Initial Datase Name**, we input **accounts** because in [Database Initialization](4_database_initialization.md), we will setup the required data in that database for the web app.
   
   After all, review and created RDS.
   
   ![](imgs/create-db-6.png)