
### Using the Sameple DataBase as Below, 
For the examples, assume a simple PostgreSQL database with a table called `cars`:

# PostgreSQL Quick Reference Sheet

Quick reference for common PostgreSQL commands and statements, with descriptions, example commands, and outputs based on a sample `cars` table:

```sql
CREATE TABLE cars (
    id SERIAL PRIMARY KEY,
    color VARCHAR(50),
    size VARCHAR(50),
    price INTEGER
);
INSERT INTO cars (color, size, price) VALUES
    ('Red', 'Small', 10000),
    ('Blue', 'Big', 20000),
    ('Red', 'Medium', 15000),
    ('Blue', 'Small', 12000),
    ('Green', 'Big', 25000);
```

| Tasks | Commands/Statements | Description | Example Command | Example Output |
|-------|---------------------|-------------|-----------------|----------------|
| Create Database | `CREATE DATABASE` | Creates a new database. | `CREATE DATABASE car_dealership;` | (Database created, no output) |
| Create Table | `CREATE TABLE` | Creates a new table with specified columns. | `CREATE TABLE cars (id SERIAL PRIMARY KEY, color VARCHAR(50), size VARCHAR(50), price INTEGER);` | (Table created, no output) |
| Insert Data | `INSERT INTO` | Adds new rows to a table. | `INSERT INTO cars (color, size, price) VALUES ('Yellow', 'Medium', 18000);` | (Row inserted, no output) |
| Select All Data | `SELECT *` | Retrieves all columns from a table. | `SELECT * FROM cars;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 1  | Red   | Small  | 10000 \n 2  | Blue  | Big    | 20000 \n 3  | Red   | Medium | 15000 \n 4  | Blue  | Small  | 12000 \n 5  | Green | Big    | 25000 ` |
| Select Specific Columns | `SELECT column1, column2` | Retrieves specified columns. | `SELECT color, price FROM cars;` | ` color | price  \n-------+--------\n Red   | 10000 \n Blue  | 20000 \n Red   | 15000 \n Blue  | 12000 \n Green | 25000 ` |
| Filter Rows | `WHERE` | Filters rows based on a condition. | `SELECT * FROM cars WHERE price > 15000;` | ` id | color | size | price  \n----+-------+------+--------\n 2  | Blue  | Big  | 20000 \n 5  | Green | Big  | 25000 ` |
| Sort Results | `ORDER BY` | Sorts results by specified column(s). | `SELECT * FROM cars ORDER BY price DESC;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 5  | Green | Big    | 25000 \n 2  | Blue  | Big    | 20000 \n 3  | Red   | Medium | 15000 \n 4  | Blue  | Small  | 12000 \n 1  | Red   | Small  | 10000 ` |
| Group Data | `GROUP BY` | Groups rows by column(s) for aggregation. | `SELECT color, COUNT(*), AVG(price) FROM cars GROUP BY color;` | ` color | count |        avg        \n-------+-------+-------------------\n Blue  |   2   | 16000.0000000000 \n Green |   1   | 25000.0000000000 \n Red   |   2   | 12500.0000000000 ` |
| Aggregate Functions | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` | Performs calculations on grouped data. | `SELECT MAX(price) FROM cars;` | `  max   \n--------\n 25000 ` |
| Join Tables | `JOIN` | Combines rows from multiple tables based on a condition. | `CREATE TABLE types (color VARCHAR(50), type VARCHAR(50));\nINSERT INTO types VALUES ('Red', 'Sport'), ('Blue', 'Sedan');\nSELECT c.color, c.price, t.type FROM cars c LEFT JOIN types t ON c.color = t.color;` | ` color | price  |  type  \n-------+--------+--------\n Red   | 10000 | Sport \n Red   | 15000 | Sport \n Blue  | 20000 | Sedan \n Blue  | 12000 | Sedan \n Green | 25000 | (null) ` |
| Update Data | `UPDATE` | Modifies existing rows in a table. | `UPDATE cars SET price = 11000 WHERE id = 1;` | (Row updated, no output) |
| Delete Data | `DELETE FROM` | Removes rows from a table. | `DELETE FROM cars WHERE price < 12000;` | (Rows deleted, no output) |
| Drop Table | `DROP TABLE` | Deletes a table and its data. | `DROP TABLE cars;` | (Table dropped, no output) |
| Drop Database | `DROP DATABASE` | Deletes an entire database. | `DROP DATABASE car_dealership;` | (Database dropped, no output) |
| Add Column | `ALTER TABLE ADD` | Adds a new column to a table. | `ALTER TABLE cars ADD year INTEGER;` | (Column added, no output) |
| Drop Column | `ALTER TABLE DROP` | Removes a column from a table. | `ALTER TABLE cars DROP year;` | (Column dropped, no output) |
| Rename Column | `ALTER TABLE RENAME COLUMN` | Renames a column in a table. | `ALTER TABLE cars RENAME COLUMN size TO car_size;` | (Column renamed, no output) |
| Change Data Type | `ALTER TABLE ALTER COLUMN` | Modifies the data type of a column. | `ALTER TABLE cars ALTER COLUMN price TYPE BIGINT;` | (Data type changed, no output) |
| Add Constraint | `ALTER TABLE ADD CONSTRAINT` | Adds a constraint (e.g., primary key, foreign key). | `ALTER TABLE cars ADD CONSTRAINT positive_price CHECK (price > 0);` | (Constraint added, no output) |
| Create Index | `CREATE INDEX` | Creates an index to improve query performance. | `CREATE INDEX idx_color ON cars(color);` | (Index created, no output) |
| Drop Index | `DROP INDEX` | Deletes an index. | `DROP INDEX idx_color;` | (Index dropped, no output) |
| Distinct Values | `DISTINCT` | Retrieves unique values from a column. | `SELECT DISTINCT color FROM cars;` | ` color \n-------\n Red   \n Blue  \n Green ` |
| Limit Rows | `LIMIT` | Restricts the number of rows returned. | `SELECT * FROM cars LIMIT 2;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 1  | Red   | Small  | 10000 \n 2  | Blue  | Big    | 20000 ` |
| Offset Rows | `OFFSET` | Skips a specified number of rows before returning results. | `SELECT * FROM cars OFFSET 2 LIMIT 2;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 3  | Red   | Medium | 15000 \n 4  | Blue  | Small  | 12000 ` |
| Case Statement | `CASE` | Applies conditional logic in queries. | `SELECT color, price, CASE WHEN price > 15000 THEN 'Expensive' ELSE 'Affordable' END AS price_category FROM cars;` | ` color | price  | price_category \n-------+--------+----------------\n Red   | 10000 | Affordable \n Blue  | 20000 | Expensive \n Red   | 15000 | Affordable \n Blue  | 12000 | Affordable \n Green | 25000 | Expensive ` |
| Handle Nulls | `COALESCE` | Returns the first non-null value in a list. | `SELECT color, COALESCE(year, 2023) AS year FROM cars;` | ` color | year \n-------+------\n Red   | 2023 \n Blue  | 2023 \n Red   | 2023 \n Blue  | 2023 \n Green | 2023 ` |
| Check Nulls | `IS NULL` | Filters rows where a column is null. | `SELECT * FROM cars WHERE year IS NULL;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 1  | Red   | Small  | 10000 \n 2  | Blue  | Big    | 20000 \n 3  | Red   | Medium | 15000 \n 4  | Blue  | Small  | 12000 \n 5  | Green | Big    | 25000 ` |
| Like Pattern Matching | `LIKE` | Filters rows based on pattern matching. | `SELECT * FROM cars WHERE color LIKE 'B%';` | ` id | color | size  | price  \n----+-------+-------+--------\n 2  | Blue  | Big   | 20000 \n 4  | Blue  | Small | 12000 ` |
| In List | `IN` | Filters rows where a column matches any value in a list. | `SELECT * FROM cars WHERE color IN ('Red', 'Green');` | ` id | color |  size  | price  \n----+-------+--------+--------\n 1  | Red   | Small  | 10000 \n 3  | Red   | Medium | 15000 \n 5  | Green | Big    | 25000 ` |
| Between Range | `BETWEEN` | Filters rows where a column is within a range. | `SELECT * FROM cars WHERE price BETWEEN 12000 AND 20000;` | ` id | color |  size  | price  \n----+-------+--------+--------\n 2  | Blue  | Big    | 20000 \n 3  | Red   | Medium | 15000 \n 4  | Blue  | Small  | 12000 ` |
| Subquery | `(SELECT ...)` | Uses a query within another query. | `SELECT * FROM cars WHERE price > (SELECT AVG(price) FROM cars);` | ` id | color | size | price  \n----+-------+------+--------\n 2  | Blue  | Big  | 20000 \n 5  | Green | Big  | 25000 ` |
| Union Results | `UNION` | Combines results of two queries, removing duplicates. | `SELECT color FROM cars WHERE size = 'Small' UNION SELECT color FROM cars WHERE size = 'Big';` | ` color \n-------\n Red   \n Blue  \n Green ` |
| Transaction Start | `BEGIN` | Starts a transaction block. | `BEGIN;` | (Transaction started, no output) |
| Commit Transaction | `COMMIT` | Saves changes made in a transaction. | `COMMIT;` | (Changes committed, no output) |
| Rollback Transaction | `ROLLBACK` | Reverts changes made in a transaction. | `ROLLBACK;` | (Changes reverted, no output) |
| Grant Permissions | `GRANT` | Assigns privileges to users. | `GRANT SELECT ON cars TO user1;` | (Permission granted, no output) |
| Revoke Permissions | `REVOKE` | Removes privileges from users. | `REVOKE SELECT ON cars FROM user1;` | (Permission revoked, no output) |
| Vacuum Database | `VACUUM` | Reclaims storage and optimizes database. | `VACUUM cars;` | (Database vacuumed, no output) |
| Analyze Table | `ANALYZE` | Updates statistics for query planner. | `ANALYZE cars;` | (Statistics updated, no output) |


> 
