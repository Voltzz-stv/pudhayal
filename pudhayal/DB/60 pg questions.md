https://youtu.be/Y1ZU1NU7wT8?si=OmMZpfIcGLtViW8l
## I. Questions for Freshers or Beginners

The first category covers questions meant for beginners or freshers.

**1. What is PostgreSQL?** PostgreSQL, also called Postgres, is a **free object relational database management system (ORDBMS)**. It is a strong database management system that integrates fundamental concepts, allowing users to extend the database or utilize it efficiently.

**2. What are the primary applications of PostgreSQL?** PostgreSQL enables users to perform all the **CRUD operations** (create, update, and delete the tables). You can also manipulate, modify, and access the data in a table. Furthermore, it allows you to summarize and retrieve the required information from a single table or multiple tables.

**3. What are the benefits of PostgreSQL?** PostgreSQL offers **excellent scalability and performance**. It efficiently manages massive amounts of data and parallel connections. It provides advanced features like support for **complex data types, geospatial data, and full-on text search**. Crucially, it supports data integrity, reliability, and **ACID properties** (Atomicity, Consistency, Isolation, and Duration).

**4. What are the important features of PostgreSQL?** PostgreSQL is **endorsed by all major operating systems** (Windows, Linux, Mac OS). It is an object relational database (ORDBMS), combining object-oriented and relational databases. It also supports **procedural languages, Multiversion Concurrency Control (MVCC)**, and includes **nested transactions**.

**5. How do we install PostgreSQL?** The installation process involves several steps:

1. Go to the official PostgreSQL website and select the version based on the operating system.
2. Execute the installer, follow on-screen instructions, and specify the installation directory/super user password.
3. Choose the components to install (Server, GUI, command line tools).
4. Finish the installation process and verify that PostgreSQL has been correctly installed. (The latest version as of September 26, 2024, was PostgreSQL 17).

**6. What is a schema?** In PostgreSQL (or any SQL database), a schema contains tables along with **views, data types, indexes, constraints, functions, and sequences**.

**7. Define a constraint in PostgreSQL.** A constraint is a **group of conditions that define the kind of data that acts as input** to every column of the table. Constraints assure data integrity and help avoid unnecessary actions.

**8. Define a join in PostgreSQL.** Joins are used for **combining and retrieving the records from two or more tables**. PostgreSQL utilizes SQL joins for these operations, including inner join, right join, left join, and full join.

**9. What is a primary key?** A primary key is the column or a group of columns that **uniquely identifies every row in the table**. It assures integrity and uniqueness. A primary key follows two rules: its value must be unique, and it must **not include null values**. Only one primary key can be defined per table.

**10. What is a foreign key?** A foreign key is a column or group of columns that **sets up the link between two tables**, depicting the relationship between the reference (parent) table and the referencing (child) table. It assures referential integrity. (The basic difference between a primary key and a foreign key is that a primary key allows only unique and non-null values, while a foreign key offers shared keys between two or more tables).

**11. Can we run PostgreSQL on the cloud?** **Yes**, PostgreSQL can be run on all famous cloud providers, including **AWS (Amazon Web Services), Google Cloud Platform (GCP), and Microsoft Azure**.

**12. What is a view?** A view **depicts the query result to one or multiple inherent tables**. Views simplify difficult queries, as they are defined once and can be directly queried.

**13. Explain normalization.** Normalization is a mechanism used to **create or modify databases and tables** for handling inefficiencies related to data storage, query processing, or data modification. It involves multiple steps for **reducing data complexity and redundancy**.

**14. What is a transaction in a database?** A transaction is a **sequence of database operations considered as a single logical unit**. It assures the **ACID properties** (atomicity, isolation, durability, and consistency). If any part of the transaction fails, all modifications can be rolled back to maintain data integrity. (Transactions can be handled internally through the autocommit mode or explicitly using `BEGIN`, `ROLLBACK`, and `COMMIT` statements).

**15. What is PL/Python?** PL/Python is a **procedural language** that PostgreSQL provides support for.

**16. What purpose does PGAdmin in the PostgreSQL Server have?** PGAdmin is a **data administration tool**. It serves the purpose of retrieving, developing, testing, and maintaining databases.

**17. How can we add new values to a particular table?** New values are added using the **`INSERT INTO`** statement. (Note: A database can be created using the `CREATE DATABASE` SQL command or the GUI interface. A database can be deleted using `DROP DATABASE` or `DROP DB` statements.)

**18. How can we create a backup of the database in PostgreSQL?** There are several methods for performing a backup: the **online backup technique, SQL dumps**, and **file system level backup**.

**19. How can we enhance the query performance in the PostgreSQL?** Strategies to enhance query performance include:

- Performing **indexing**, which is very helpful in queries that include the `WHERE` clause.
- **Partitioning** large tables into smaller tables for easier handling.
- Developing SQL statements to reduce processing overhead, for example, by **preventing unrequired columns in `SELECT` statements**.
- **Tuning server parameters** to maximize memory utilization.

**20. How can we handle errors in PostgreSQL?** Errors can be handled in two ways:

1. By using **callback functions** to define a particular behavior in case of warnings and errors through the `WHENEVER` method.
2. By retrieving **detailed information from the SQL variable** when warnings and errors arise during query execution.

---

## II. Questions for Experienced or Intermediate Candidates

This section covers questions meant for candidates with at least two to three years of experience.

**21. Describe triggers.** Triggers (also called callback functions) are specifications a database automatically implements when a specific operation is carried out. They are normally defined to execute either **before or after `INSERT`, `UPDATE`, or `DELETE` operations**. Triggers ensure that **data integrity is preserved** while modifying the database.

**22. Explain Multiversion Concurrency Control or MVCC.** MVCC is an **advanced technique of PostgreSQL** that improves database performance in multi-user scenarios. With MVCC, every transaction views a **snapshot of the database** from a previous point in time. This feature secures the transaction from seeing inconsistent data updated by concurrent transactions on the similar data rows.

**23. What are the different logging mechanisms available in PostgreSQL and what is their purpose?** PostgreSQL provides different kinds of logging mechanisms:

- **Error logs** to capture errors and warnings.
- **Query logs** to record executed queries for performance analysis and debugging.
- **Connection logs** to track connection attempts and disconnections to the database.

**24. Explain the difference between inner join and left join with example.** An **Inner Join** returns **only rows with matching values in both tables**. A **Left Join** returns **all rows from the left table** and the matching rows from the right table, using nulls for non-matching rows.

- _Inner Join Example Query:_ `SELECT * FROM employees INNER JOIN departments ON employees.Department ID = Departments.ID`.
- _Left Join Example Query:_ `SELECT * FROM employees LEFT JOIN departments ON employees.Department ID = Departments.ID`.

**25. Write a SQL query to find the total number of employees in each of the Departments.** The query uses the `COUNT` function and the `GROUP BY` clause. **Query:** `SELECT Department ID, COUNT(*) FROM employees GROUP BY Department ID`.

**26. What are indexes in PostgreSQL and how do they improve the query performance?** Indexes are special database objects that **improve the speed of data retrieval operations**. They create a data structure that allows for faster searches. They significantly improve performance by **reducing the amount of data that needs to be scanned**, although they can introduce some overhead during write operations.

**27. Write an SQL query to update the salary of an employee with a specific ID.** The query uses the `UPDATE` and `SET` statements with a `WHERE` clause. **Query:** `UPDATE employees SET salary = 80,000 WHERE ID = 123`.

**28. Explain the use of GROUP BY Clause with an example.** The `GROUP BY` clause is used to **aggregate the data based on one or more columns**. It is often used with aggregate functions such as `COUNT`, `SUM`, or `AVERAGE`. **Example Query:** `SELECT Department ID, AVG(salary) FROM employees GROUP BY Department ID`.

**29. What are subqueries and how they can be used in PostgreSQL?** Subqueries are **nested queries** (one query inside another) that can be included in the `SELECT`, `FROM`, or `WHERE` clauses. They perform complex queries in a modular way. Subqueries can be used to filter the data, compute aggregate values, or generate temporary results for joining with other tables.

**30. Write an SQL query to find the second highest salary from the employees table.** This query requires finding the maximum salary that is less than the overall maximum salary. **Query:** `SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees)`.

**31. Write an SQL query to list all of the employees who joined in the last year.** This query utilizes date functions like `NOW()` and `INTERVAL`. **Query:** `SELECT * FROM employees WHERE join_date >= NOW() - INTERVAL '1 year'`.

**32. Write an SQL query to create a view that shows the average salary by department.** The query uses the `CREATE VIEW` statement along with the `AVG` aggregate function and `GROUP BY`. **Query:** `CREATE VIEW average_salary_by_department AS SELECT Department ID, AVG(salary) FROM employees GROUP BY Department ID`.

**33. Write an SQL query to find the all the employees whose name start with the letter A.** This query uses the `LIKE` operator with the wildcard (`%`). **Query:** `SELECT * FROM employees WHERE name LIKE 'A%'`.

**34. Write an SQL query to perform the full text search on a documents table.** PostgreSQL's full text search feature uses the **`TS_VECTOR`** and **`TS_QUERY`** data types, along with the **match operator (`@@`)**. **Query:** `SELECT * FROM documents WHERE TO_TSVECTOR(content) @@ TO_TSQUERY('search term')`.

**35. What are the common Performance Tuning techniques in PostgreSQL?** Common techniques include **indexing** (to speed up data retrieval), using query optimization tools like **`EXPLAIN ANALYZE`** (to identify slow queries), and regular maintenance tasks such as **vacuuming and analyzing**.

**36. Explain the difference between a view and a materialized view in PostgreSQL.** A **view** is a **virtual table** that dynamically retrieves data, making it suitable for real-time data. A **materialized view** physically stores the result set of a query, allowing faster access, but it requires **manual refreshes**. Materialized views are ideal for performance optimization in read-heavy scenarios.

**37. What are the stored procedures and how can you create one in PostgreSQL?** Stored procedures are **reusable SQL code blocks** that perform a specific task. They are created using the **`CREATE PROCEDURE`** statement, defining the procedure name, parameters, and the SQL code block to encapsulate the logic.

**38. What are functions in PostgreSQL and how they can be used to extend the SQL functionality?** Functions in PostgreSQL are **reusable SQL or PL/pgSQL code blocks** that encapsulate logic for tasks like calculations, data manipulation, and complex queries. They extend SQL functionality by providing complex or custom operations and enhance modularity and code reuse.

**39. Explain the concept of replication in PostgreSQL and its benefits for the data availability.** Replication involves **copying data from a master server to one or more standby (slave) servers**. This can be synchronous or asynchronous. Replication is done to improve **data availability, load balancing, and disaster recovery**, preventing a single point of failure.

**40. What are some of the best practices for Designing and maintaining a PostgreSQL database?** Best practices include:

- **Normalizing the data** to reduce redundancy.
- Using appropriate data types and **applying indexes strategically**.
- Regularly **backing up data**.
- **Monitoring performance** to identify bottlenecks.

---

## III. Questions for More Experienced or Advanced Candidates

This final section covers questions intended for more experienced candidates (at least 3 to 5 years of experience).

**41. Write a query that returns the total number of bookings in the last 90 days, last 365 days, and the overall number of bookings from a `vacations_booking` table.** This query uses the aggregate function `SUM` with conditional `CASE` statements based on date intervals. **Query Structure:**

```
SELECT
    SUM(CASE WHEN check_in_date >= DATE_ADD(CURRENT_DATE, INTERVAL '3 month') THEN 1 ELSE 0 END) AS num_bookings_last_90_days,
    SUM(CASE WHEN check_in_date >= DATE_ADD(CURRENT_DATE, INTERVAL '1 year') THEN 1 ELSE 0 END) AS num_bookings_last_365_days,
    COUNT(reservation_IDs) AS num_bookings_total
FROM bookings
```

(Note: The specific date arithmetic functions used in the source query template—`DATE_ADD`—may be syntactically adjusted based on the specific PostgreSQL version, though the concept relies on comparing the `check_in_date` to the current date minus an `INTERVAL`).

**42. Design a cost-effective data analytics solution for storing and querying 600 million daily clickstream events from Kafka with a 2-year retention period.** A cost-effective solution involves using a combination of **Apache Kafka** (for streaming) and **Apache Hadoop** (for storing and analyzing the data). Alternatively, for cloud infrastructure, **Amazon S3** can be used for long-term storage. PostgreSQL can be used for querying and data analytics by leveraging **columnar storage** and implementing **data partitioning** (by date or user ID) to optimize performance. To manage storage costs for the 2-year retention period, you must **regularly compress and archive the older data**.

**43. Describe the different types of user accounts and access control mechanisms in PostgreSQL.** **Roles** represent users or groups and are assigned privileges for database objects, such as `SELECT`, `INSERT`, and `UPDATE`. **User roles** can log in, while **group roles** manage privileges collectively. Authentication methods include passwords, GSS API, SSPI, LDAP, and certificates. Additionally, **Row Level Security (RLS)** allows for fine-grained access control by restricting which rows a user can access.

**44. Explain how you would migrate data from one database system to PostgreSQL.**

1. **Export** the source database schema and data using tools like `pg_dump` or equivalent tools for other databases.
2. **Create the schema** in PostgreSQL using the exported SQL script and then **import the data** (using tools like PGAdmin, psql, or third-party ETL tools).
3. **Verify the data integrity** once the migration has been completed.

**45. How can you stop a PostgreSQL Server? Like, can you stop a particular database in the PostgreSQL SQL cluster?** To stop a PostgreSQL Server, the command depends on the operating system:

- **Windows:** `pg_ctl -D [path of the database directory] stop`.
- **Linux:** `sudo service postgresql stop`.
- **Mac OS:** `pg_ctl -D [path] stop` (e.g., `/user/local/var/postgres`). Regarding the second part: **No, PostgreSQL does not allow the user to stop a specific database in the cluster**.

**46. Why explicitly put foreign key constraints? When should you consider `CASCADE DELETE` or `SET NULL`?** Foreign key constraints are used to ensure **data integrity** by enforcing relationships between tables, preventing orphaned records, and maintaining consistency.

- Use **`CASCADE DELETE`** when you want related records to be automatically removed when the parent record is deleted.
- Use **`SET NULL`** when you want to retain related records but nullify the foreign key value upon the parent's deletion.

**47. Write a query to find all of the users that are currently 'excited' and have never been 'bored' with a campaign.** This query requires using a nested query with the `NOT IN` clause. **Query:** `SELECT DISTINCT user_ID FROM ad_Impressions WHERE impression_ID = 'excited' AND user_ID NOT IN (SELECT user_ID FROM ad_Impressions WHERE impression_ID = 'bored')`.

**48. How to handle exceptions in PL/pgSQL?** Exceptions are handled using the **`EXCEPTION`** keyword within a PL/pgSQL block (`DO $$ BEGIN... END $$;`). The required action is defined based on the error condition (e.g., `WHEN unique_violation THEN RAISE NOTICE 'Duplicate key error'`).

**49. Explain the concept of JSON data types in PostgreSQL.** PostgreSQL supports **JSON** and **JSONB** (binary format) data types for storing and querying semi-structured data. JSON data works in key-value pairs. JSONB is generally more efficient for indexing purposes.

**50. What does Write Ahead Logging (WAL) do?** **WAL** is a method used by PostgreSQL to ensure **data integrity and durability**. WAL works by **recording database changes in a log file before they are applied to the actual data files**. Using WAL allows PostgreSQL to recover from crashes, support data replication, and ensure durability.

**51. What is the role of VACUUM in PostgreSQL?** Vacuum is a crucial process for **managing and reclaiming disk space** occupied by deleted or outdated data, which is essential for maintaining database performance and efficiency. Vacuum performs two main tasks:

1. **Freeing up disk space:** It identifies reusable data pages (data marked as reusable by future inserts) and makes the space available.
2. **Updating statistics:** It analyzes data distribution and updates the statistics used by the query planner to choose optimal query plans, resulting in improved performance.

**52. How do you use advisory locks in PostgreSQL?** Advisory locks are **user-defined locks** that coordinate between database sessions. They are acquired and released voluntarily and do not conflict with row-level locks. They are often used for application-level synchronization.

- To acquire a lock: `SELECT pg_advisory_lock([lock ID])`.
- To release a lock: `SELECT pg_advisory_unlock([lock ID])`.

**53. How do you use the PG Bouncer connection Pooler with PostgreSQL?** PG Bouncer acts as a middle layer that manages a pool of database connections, improving scalability and performance. The steps to use it are:

1. **Install and configure** PG Bouncer on a separate server.
2. **Edit the `pgbouncer.ini` configuration file** to specify PostgreSQL servers and the pool mode (transaction or session).
3. **Start the PG Bouncer service**.
4. **Modify your application settings** to connect to PG Bouncer instead of directly connecting to PostgreSQL.

**54. What is the difference between a clustered index and a non-clustered index in PostgreSQL?** A **clustered index** is an index type that is used to **store tables or table data rows according to their key values**.

**55. What are the three phenomena that must be prevented between concurrent transactions in PostgreSQL SQL?** These three unwanted phenomena are related to transaction isolation levels:

1. **Dirty Read:** A transaction reads data written by a concurrent, uncommitted transaction.
2. **Non-Repeatable Read:** A transaction re-reads data it previously read and finds that another transaction has modified it.
3. **Phantom Read:** A transaction re-executes a query that returns a set of rows and finds that the set of rows satisfying the condition has changed due to a recently committed transaction.

**56. What do you understand by an inverted file in PostgreSQL?** An inverted file is an **index data structure** used to map the content to its location within a document or set of documents in a database. It generally includes the distinct words found in a text and a list containing the occurrences of that word. It is used in document retrieval systems to provide the **full text search**.

**57. What is the purpose of pg_stat_ssl view in PostgreSQL?** The `pg_stat_ssl` view provides information about the **current SSL/TLS connections** established within the server. It highlights statistics related to the encryption and security parameters, including the process ID, SSL/TLS version, cipher suite, and compression status.

**58. What is a hot standby in PostgreSQL and how does it work?** Hot standby is a feature that allows users to run **read-only queries on a replicated database while it is replicating data** from the primary database. This setup provides high availability and load balancing. It works in conjunction with streaming replication, where the replica continuously receives WAL records; in case of primary failure, the replica can be promoted to take over as the new primary.

**59. How do we Implement table partitioning?** Partitioning splits a large table into smaller, manageable pieces known as partitions. The steps to implement it are:

1. **Create the parent table** with all required columns, including the partitioning key.
2. **Create child tables** that inherit from the parent table, where each child table represents a partition.
3. **Define constraints** on every child table for limiting the partitioning key values.
4. **Create indexes** on the child tables for optimizing query performance. Partitioning simplifies data management and enhances query performance.

**60. How do we Implement sharding?** Sharding refers to **horizontal partitioning data throughout multiple shards or servers** to distribute the load and scale the database system. The implementation steps are:

1. **Set up Shard servers:** Create individual PostgreSQL clusters or instances for every shard.
2. **Determine the Shard strategy:** Select a strategy to partition the data (e.g., hash-based or range-based sharding).
3. **Implement the application logic:** Modify the application code or use middleware to route queries to the proper shard.
4. **Define the data distribution rules** based on the selected strategy.
5. **Manage data synchronization and consistency** throughout the shards (using mechanisms like logical replication or distributed transaction tools).