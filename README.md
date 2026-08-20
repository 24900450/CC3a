# CLOUD-DATA-STORAGE-SERVER
# Lab 5: Build Your DB Server and Interact With Your DB Using an App
## Name : SURYANARAYANAN T
## Register Number : 212224040341
## Aim

To create a highly available MySQL database using **Amazon RDS**, configure secure connectivity between an EC2 web server and the RDS database, and interact with the database through a web application.

## Algorithm

1. Open the AWS Management Console and access the VPC service.
2. Create a security group named `DB Security Group` in `Lab VPC`.
3. Configure an inbound rule to allow MySQL/Aurora traffic on port `3306` from `Web Security Group`.
4. Open Amazon RDS and create a DB subnet group named `DB-Subnet-Group`.
5. Select Availability Zones `us-east-1a` and `us-east-1b`.
6. Select the subnets with CIDR ranges `10.0.1.0/24` and `10.0.3.0/24`.
7. Create an RDS MySQL database named `lab-db`.
8. Configure the database as a **Multi-AZ DB instance** using `db.t3.micro`.
9. Configure the database name as `lab` and username as `main`.
10. Associate the database with `Lab VPC`, `DB Security Group`, and `DB-Subnet-Group`.
11. Wait until the RDS instance status becomes **Available**.
12. Copy the RDS database endpoint.
13. Open the web application using the WebServer IP address.
14. Select the **RDS** option in the web application.
15. Enter the RDS endpoint, database name, username, and password.
16. Submit the configuration to connect the web application to RDS.
17. Test the Address Book application by adding, editing, and deleting contacts.
18. Verify that the data is successfully persisted in the RDS database.

## Program

### RDS Configuration

```text
Database Engine      : MySQL
DB Instance Identifier: lab-db
Deployment            : Multi-AZ DB Instance
Instance Class        : db.t3.micro
Storage               : 20 GB General Purpose SSD
Database Name         : lab
Master Username       : main
VPC                   : Lab VPC
DB Subnet Group       : DB-Subnet-Group
Security Group        : DB Security Group
MySQL Port            : 3306
```

### Security Group Configuration

```text
Security Group Name : DB Security Group
Description         : Permit access from Web Security Group
Inbound Protocol    : TCP
Port                : 3306
Source              : Web Security Group
```

### DB Subnet Group

```text
Name        : DB-Subnet-Group
VPC         : Lab VPC

Availability Zones:
- us-east-1a
- us-east-1b

Subnets:
- 10.0.1.0/24
- 10.0.3.0/24
```

### Web Application Configuration

```text
Endpoint : <RDS endpoint>
Database : lab
Username : main
Password : <lab password>
```

> For a public GitHub repository, do not include the actual database password or other credentials.

## Output

### 1. DB Security Group

The RDS security group was successfully created with MySQL port `3306` accessible from the Web Security Group.

**Screenshot:** `images/01-db-security-group.png`

![DB Security Group](images/01-db-security-group.png)

---

### 2. DB Subnet Group

The DB subnet group was successfully created using two Availability Zones and the required subnets.

**Screenshot:** `images/02-db-subnet-group.png`

![DB Subnet Group](images/02-db-subnet-group.png)

---

### 3. RDS Database

The MySQL RDS instance `lab-db` was successfully created with a Multi-AZ deployment.

**Screenshot:** `images/03-rds-available.png`

![RDS Database](images/03-rds-available.png)

---

### 4. RDS Connection

The web application was configured with the RDS endpoint and database credentials.

**Screenshot:** `images/04-rds-connection.png`

![RDS Connection](images/04-rds-connection.png)

---

### 5. Address Book Application

The web application successfully connected to the RDS database and displayed the Address Book.

**Screenshot:** `images/05-address-book.png`

![Address Book](images/05-address-book.png)

---

### 6. CRUD Operations

Contacts were successfully added, edited, and removed through the web application, confirming that the application was interacting with the RDS database.

**Screenshot:** `images/06-crud-operation.png`

![CRUD Operations](images/06-crud-operation.png)

## Result

The **Amazon RDS MySQL database** was successfully created with **Multi-AZ high availability**. The EC2 web application was successfully connected to the RDS database through port `3306`, and CRUD operations were successfully performed using the Address Book application.

Therefore, the objective of creating an AWS-managed relational database and interacting with it through a web application was successfully achieved.
