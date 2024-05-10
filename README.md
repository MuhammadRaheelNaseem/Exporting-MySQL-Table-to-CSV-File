# Exporting MySQL Table to CSV File

This Lecture provides step-by-step instructions on how to export data from a MySQL table to a CSV file on your local system.

## Prerequisites

Before following the instructions, ensure you have:
- MySQL installed on your local system
- Access to a MySQL database with appropriate permissions to export data

## Command 1: Export Data Using `SELECT INTO OUTFILE`

Run the following SQL command to export data from the `city` table to a CSV file named `abc.csv`:

```sql
SELECT * FROM city INTO OUTFILE 'abc.csv' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\n';
```

If you encounter the error `ERROR 1290 (HY000): The MySQL server is running with the --secure-file-priv option`, proceed to the next step.

## Command 2: Handling Security Restrictions

Run the following SQL command to determine the directory where MySQL allows files to be written:

```sql
SHOW VARIABLES LIKE "secure_file_priv";
```

## Command 3: Export Data to Allowed Directory

Use the directory obtained from the previous command to export data to a CSV file:

```sql
SELECT * FROM city INTO OUTFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/abc.csv' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\n';
```

## Program 4: Export Data with Field Names Using Python

If you want to save rows data with header field (column title), you can use the following Python program:

```python
import csv
import mysql.connector

# Connect to MySQL database
db = mysql.connector.connect(host="localhost", user="root", passwd="admin", db="world")
cursor = db.cursor()

# Retrieve column names from the city table
cursor.execute("SHOW COLUMNS FROM city")  
column_names = [row[0] for row in cursor.fetchall()]

# Retrieve data from the city table
cursor.execute("SELECT * FROM city")
data = cursor.fetchall()

# Write data to CSV file with column names as header
with open('abcc.csv', 'w', newline='') as csvfile:
    csvwriter = csv.writer(csvfile)
    csvwriter.writerow(column_names)  # Write column names
    csvwriter.writerows(data)  # Write data
    print("Data created successfully")

# Close connections
cursor.close()
db.close()
```

Run the Python program to export data from the `city` table along with column names to a CSV file named `abcc.csv`.
