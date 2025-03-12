# MySQL Practice with Amazon RDS on AWS

## Overview
This guide provides step-by-step instructions to set up and practice MySQL with Amazon RDS on AWS. The process includes creating a VPC, setting up EC2 and RDS instances, and executing database operations using Python scripts.

## Steps to Follow

### 1. Create a VPC (Virtual Private Cloud)
- Configure a custom VPC to isolate AWS resources securely.

### 2. Set Up Subnets
- **Public Subnet**: Allows EC2 to access the internet.
- **Private Subnet**: Provides a secure environment for RDS.

### 3. Configure Security Groups
- **EC2 Security Group**: Allows SSH (port 22) and MySQL (port 3306) traffic.
- **RDS Security Group**: Allows inbound connections from the EC2 instance.

### 4. Create an Internet Gateway (IGW) & Route Table
- Attach the IGW to the VPC.
- Modify the route table to enable internet access for the public subnet.

### 5. Launch an EC2 Instance
- Choose an appropriate instance type.
- Install MySQL client using:
  ```sh
  sudo apt update && sudo apt install mysql-client -y
  ```

### 6. Create an RDS MySQL Database
- Configure an RDS MySQL instance in the private subnet.
- Retrieve the **RDS endpoint** after creation.

### 7. Connect EC2 to RDS
- Create `venv`.
- Use the MySQL client to connect to the RDS instance:
  ```sh
  mysql -h <RDS-endpoint> -u admin -p
  ```

### 8. Create a Database and Table
- Run the following SQL commands:
  ```sql
  CREATE DATABASE customerdb;
  USE customerdb;
  CREATE TABLE customer (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(255),
      address VARCHAR(255)
  );
  ```

### 9. Python Scripts for Database Operations

#### **Insert Data (insert.py)**
```python
import mysql.connector

conn = mysql.connector.connect(
    host="your-endpoint",
    user="admin",
    password="your-password",
    database="customerdb"
)

cursor = conn.cursor()

sql = "INSERT INTO customer (name, address) VALUES (%s, %s)"
val = ("Pham Chi Vy", "HUST")

cursor.execute(sql, val)
conn.commit()
conn.close()

print("Data inserted successfully!")
```

#### **Read Data (read.py)**
```python
import mysql.connector

conn = mysql.connector.connect(
    host="your-endpoint",
    user="admin",
    password="your-password",
    database="customerdb"
)

cursor = conn.cursor()

cursor.execute("SELECT * FROM customer")
results = cursor.fetchall()

for row in results:
    print(row)
```

### 10. Execute the Python Scripts
Run the following commands in your EC2 instance:
```sh
python3 insert.py
python3 read.py
```

## Expected Output
The `insert.py` script should insert a new record into the `customer` table. The `read.py` script should retrieve and display all records from the table.
![](assets/Apache.png)
![](assets/Apache.png)
## Conclusion
This guide helps set up and practice MySQL with Amazon RDS using AWS infrastructure. You can further enhance security by implementing IAM roles and using parameter groups to fine-tune database performance.

