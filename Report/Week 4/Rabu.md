````markdown
# Week 04 - SQL & Database Fundamental

## 1. Overview

During Week 04 of the Industry Simulation Program – Data Analyst, I focused on learning SQL and database fundamentals.

The activities were carried out through several practical projects, starting from basic SQL operations and progressing to data aggregation, conditional analysis, calculated columns, and joining data from multiple tables.

The main objective of this week was to understand how SQL can be used to retrieve, process, summarize, and combine data before it is used for further analysis.

---

## 2. Objectives

The main objectives of Week 04 were:

- Understand the fundamentals of SQL and relational databases.
- Retrieve data from database tables using SQL.
- Filter data based on specific conditions.
- Perform aggregation and grouping.
- Use conditional statements with `CASE WHEN`.
- Create calculated columns.
- Understand relationships between database tables.
- Combine data from multiple tables using `JOIN`.
- Execute and validate SQL queries using MySQL/MariaDB.
- Document the results and evidence of each project in GitHub.

---

## 3. Tools and Environment

The following tools were used throughout the projects:

| Tool | Purpose |
|---|---|
| XAMPP | Local database development environment |
| MySQL / MariaDB | Database Management System |
| phpMyAdmin | Database management and SQL query execution |
| SQL | Query language for retrieving and processing data |
| GitHub | Project documentation and version control |

---

# 4. Project 03 - SQL Fundamental

Project 03 focused on the fundamental concepts of SQL and retrieving data from database tables.

The activities included:

- Using `SELECT`
- Selecting specific columns
- Filtering records
- Using `WHERE`
- Using comparison operators
- Using logical conditions
- Sorting query results

The project introduced the basic process of retrieving data from a database according to specific requirements.

For example:

```sql
SELECT *
FROM table_name
WHERE condition;
````

This concept is important because a Data Analyst does not always need to retrieve all available records. SQL can be used to retrieve only the data required for a particular analysis.

### Learning Outcome

After completing Project 03, I understood how to:

* Retrieve data from a database table.
* Select specific columns.
* Filter records using conditions.
* Apply basic SQL syntax.
* Execute SQL queries using phpMyAdmin.

---

# 5. Project 04 - SQL Aggregation & Analysis

Project 04 continued the SQL learning process by introducing aggregation and data analysis techniques.

The main concepts practiced were:

* `GROUP BY`
* `SUM()`
* `AVG()`
* Aggregate functions
* `CASE WHEN`
* Calculated columns
* Data grouping

Instead of only displaying individual records, the data could be summarized into more meaningful information.

For example:

```sql
SUM()
```

can be used to calculate a total value, while:

```sql
AVG()
```

can be used to calculate an average value.

The project also introduced `CASE WHEN` for classifying data based on specific conditions.

Example:

```sql
CASE
    WHEN total >= 50000 THEN 'Target Achieved'
    WHEN total <= 20000 THEN 'Less performed'
    ELSE 'Follow Up'
END
```

### Learning Outcome

Through Project 04, I learned how SQL can transform transaction-level data into summarized information.

The data could be grouped and analyzed to obtain information such as:

* Total values
* Average values
* Data grouped by category
* Performance classifications
* Calculated results

---

# 6. Project 05 - SQL Aggregation & Conditional Analysis

Project 05 focused on further practicing aggregation, calculated columns, and conditional analysis using transaction data.

The project used the following tables:

```text
orders
orderdetails
```

The activities included:

* Calculating total revenue.
* Calculating total quantity.
* Grouping data based on products.
* Calculating average transaction values.
* Using `CASE WHEN` for revenue classification.
* Working with transaction and transaction-detail data.

One of the calculated columns used was:

```sql
quantityOrdered * priceEach AS total
```

This allowed the transaction value to be calculated directly through SQL.

### Learning Outcome

Project 05 helped me understand how SQL can be used not only to retrieve data, but also to perform basic analysis directly inside the database.

The queries can be used to answer analytical questions such as:

* What is the total revenue?
* How many products were sold?
* What is the average transaction value?
* How does the data compare between products?
* How can transaction values be classified?

---

# 7. Project 06 - SQL JOIN

Project 06 focused on combining data from multiple related tables using SQL JOIN operations.

The main tables used were:

```text
tr_penjualan
ms_produk
```

The relationship between the tables was based on the `kode_produk` column:

```text
tr_penjualan.kode_produk
        =
ms_produk.kode_produk
```

The `kode_produk` column was used as the key column to connect related records between the transaction and product tables.

## Quiz 1 - INNER JOIN

The first exercise demonstrated how to combine the two tables using `INNER JOIN`.

```sql
SELECT
    tr_penjualan.*,
    ms_produk.*
FROM tr_penjualan
INNER JOIN ms_produk
    ON tr_penjualan.kode_produk = ms_produk.kode_produk;
```

The project also demonstrated an alternative approach using `WHERE`:

```sql
SELECT
    tr_penjualan.*,
    ms_produk.*
FROM tr_penjualan, ms_produk
WHERE tr_penjualan.kode_produk = ms_produk.kode_produk;
```

Both queries use the same matching condition:

```text
tr_penjualan.kode_produk = ms_produk.kode_produk
```

The exercise demonstrated how related records can be combined based on a matching key column.

## Quiz 2 - JOIN and Calculated Column

The second exercise extended the JOIN concept by selecting specific columns from both tables and creating a calculated `total` column.

The result contains:

```text
kode_transaksi
kode_pelanggan
kode_produk
nama_produk
harga
qty
total
```

The `total` value was calculated using:

```text
total = harga × qty
```

The SQL query used was:

```sql
SELECT
    tr_penjualan.kode_transaksi,
    tr_penjualan.kode_pelanggan,
    tr_penjualan.kode_produk,
    ms_produk.nama_produk,
    ms_produk.harga,
    tr_penjualan.qty,
    ms_produk.harga * tr_penjualan.qty AS total
FROM tr_penjualan
INNER JOIN ms_produk
    ON tr_penjualan.kode_produk = ms_produk.kode_produk;
```

### Learning Outcome

After completing Project 06, I understood how to:

* Identify key columns between related tables.
* Combine data from multiple tables.
* Use `INNER JOIN`.
* Define relationships using `JOIN ... ON`.
* Use `WHERE` as an alternative matching condition.
* Use table prefixes when working with multiple tables.
* Create calculated columns from existing data.

---

# 8. Overall Learning Flow

The learning process throughout Project 03 to Project 06 progressed from basic SQL operations to relational data processing.

```text
SQL Fundamentals
        ↓
SELECT & Filtering
        ↓
Aggregation
        ↓
GROUP BY & CASE WHEN
        ↓
Calculated Columns
        ↓
Understanding Table Relationships
        ↓
INNER JOIN
        ↓
Combining Data from Multiple Tables
```

This progression helped build an understanding of how SQL can be used as part of a data analysis workflow.

---

# 9. Documentation and Evidence

Each project was documented in the GitHub repository.

The project documentation contains:

* SQL query files.
* Database datasets.
* Markdown documentation.
* Screenshots of query execution.
* Project structure and evidence.

Screenshots were used as evidence that the SQL queries had been executed successfully through the database environment.

The documentation also provides an organized record of the learning process and results obtained during the projects.

---

# 10. Skills Developed

After completing Project 03 to Project 06, I developed the following skills:

### SQL Fundamentals

* Writing `SELECT` queries.
* Selecting specific columns.
* Filtering data using `WHERE`.
* Applying logical and comparison conditions.
* Sorting query results.

### Data Aggregation

* Using `SUM()`.
* Using `AVG()`.
* Using `GROUP BY`.
* Creating calculated columns.
* Using `CASE WHEN`.

### Relational Database

* Understanding key columns.
* Understanding relationships between tables.
* Using table prefixes.
* Using `INNER JOIN`.
* Using `JOIN ... ON`.
* Combining data from multiple tables.

### Data Analysis

* Summarizing transaction data.
* Calculating transaction values.
* Grouping data.
* Creating classifications.
* Combining transaction and product information for analysis.

---

# 11. Project Summary

| Project    | Main Focus                         | Main Learning Outcome                                       |
| ---------- | ---------------------------------- | ----------------------------------------------------------- |
| Project 03 | SQL Fundamental                    | Retrieving and filtering data                               |
| Project 04 | Aggregation & Analysis             | Summarizing and grouping data                               |
| Project 05 | Aggregation & Conditional Analysis | Processing transaction data and creating calculated results |
| Project 06 | SQL JOIN                           | Combining data from related tables                          |

---

# 12. Conclusion

During Week 04, I learned the fundamental concepts of SQL and relational databases through four practical projects.

The learning process started with basic data retrieval and filtering in Project 03. It then progressed to aggregation, grouping, conditional statements, and calculated columns in Project 04 and Project 05.

Project 06 introduced relational data and SQL JOIN operations, allowing data from the `tr_penjualan` and `ms_produk` tables to be combined using the `kode_produk` key column.

Overall, these projects provided a practical foundation for using SQL as a Data Analyst. I learned that SQL can be used not only to retrieve data, but also to process, summarize, calculate, classify, and combine data from multiple related tables.

All project activities and results were documented in GitHub as evidence of the work completed during the Industry Simulation Program.

```
```
