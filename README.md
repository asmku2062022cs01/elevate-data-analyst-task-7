# Task 7 — Basic Sales Summary Using Python & SQLite

This project demonstrates how to create and query a tiny SQLite database using Python, summarize sales data with SQL, and visualize revenue using pandas and Matplotlib.

# Project Overview

In this task, a small sales_data.db database is created containing basic product sales.
Python is used to:

Create a SQLite table

Insert sample sales records

Run SQL queries to calculate total quantity and revenue

Load results into pandas

Visualize revenue with a bar chart

# Features

SQLite in-memory/Colab-friendly database

SQL aggregation using SUM()

pandas DataFrame for analysis

Matplotlib bar chart visualization

Simple and beginner-friendly workflow

# Technologies Used

Python

SQLite (sqlite3)

pandas

Matplotlib

Google Colab (optional)

# Code Summary
1. Create SQLite Database & Insert Data

   import sqlite3

conn = sqlite3.connect("sales_data.db")
cursor = conn.cursor()

cursor.execute('''
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY,
    product TEXT,
    quantity INTEGER,
    price REAL
)
''')

cursor.execute("DELETE FROM sales")

sample_data = [
    ('Laptop', 5, 700),
    ('Phone', 10, 300),
    ('Tablet', 7, 250),
    ('Laptop', 3, 700),
    ('Phone', 5, 300)
]

cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)", sample_data)
conn.commit()

2. Query with SQL Using pandas

   import pandas as pd

query = """
SELECT 
    product,
    SUM(quantity) AS total_qty,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""

df = pd.read_sql_query(query, conn)
conn.close()

print(df)

**Output:**

  product  total_qty  revenue
0  Laptop          8   5600.0
1   Phone         15   4500.0
2  Tablet          7   1750.0
3. Plot Revenue Bar Chart

import matplotlib.pyplot as plt

df.plot(kind='bar', x='product', y='revenue', color='skyblue', legend=False)
plt.title("Revenue by Product")
plt.xlabel("Product")
plt.ylabel("Revenue")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

# What  Learned

How to create and manage a SQLite database in Python

How to write SQL aggregation queries

How to convert SQL results into pandas DataFrames

How to visualize data with Matplotlib
