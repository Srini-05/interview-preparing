# Database

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>`.

<details><summary>Normalization</summary>

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity by dividing data into related tables. It follows normal forms (1NF, 2NF, 3NF, BCNF, 4NF, 5NF) to eliminate data anomalies.

### Normal Forms Explained:

#### 1NF (First Normal Form)
- **Rule**: Eliminate repeating groups and ensure atomic values
- **Problem Solved**: Repeating columns or multi-valued attributes
- **Example**: Instead of `phone_numbers: "123-456,789-012"` → Separate Phone table

#### 2NF (Second Normal Form)
- **Rule**: Remove partial dependencies (non-key attributes depend on part of composite key)
- **Problem Solved**: Partial dependencies
- **Example**: In `OrderDetails(order_id, product_id, order_date, product_name)` → `order_date` depends only on `order_id`, so move to Orders table

#### 3NF (Third Normal Form)
- **Rule**: Remove transitive dependencies (non-key depends on another non-key)
- **Problem Solved**: Transitive dependencies
- **Example**: In `Employee(emp_id, dept_id, dept_name, location)` → `dept_name` depends on `dept_id`, not directly on `emp_id`

### Practical Example:
**Unnormalized Table:**
```
Students: student_id, name, courses (Math, Science, History), teacher_names (John, Mary, Bob)
```

**After Normalization:**
- **Students**: student_id (PK), name
- **Courses**: course_id (PK), course_name, teacher_id (FK)
- **Enrollments**: student_id (FK), course_id (FK), enrollment_date

### Interview Explanation:
"Normalization is about organizing data to eliminate redundancy and anomalies. I follow the normal forms progressively: 1NF for atomic values, 2NF to remove partial dependencies, 3NF for transitive dependencies. In practice, I balance normalization with performance - sometimes denormalization is needed for read-heavy systems. For example, in an e-commerce system, I normalize customer and order data but might denormalize product categories for faster queries."

**Interview Tip:** Normalization reduces data duplication and anomalies. Balance with performance - denormalize for read-heavy systems.

</details>

<details><summary>Primary key vs Foreign key</summary>

A primary key uniquely identifies a record in a table, while a foreign key establishes a relationship by referencing the primary key of another table.

### Primary key
Key points:
- Must be unique
- Cannot be NULL
- Only one primary key per table
- Ensures entity integrity

Example:
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

### Foreign Key
A Foreign Key is a column that refers to the primary key of another table.
Key points:
- Can have duplicate values
- Can be NULL (unless restricted)
- A table can have multiple foreign keys
- Ensures referential integrity

Example:
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

**Interview Tip:** Primary key unique per table, foreign key links tables.

</details>

<details><summary>SQL Commands: DDL, DML, DCL, TCL</summary>

SQL commands are categorized based on their functionality:

### DDL (Data Definition Language)
Used to define/modify database structure. Auto-committed, can't be rolled back.

```sql
-- Create table
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Alter table
ALTER TABLE Users ADD COLUMN phone VARCHAR(20);
ALTER TABLE Users DROP COLUMN phone;
ALTER TABLE Users MODIFY COLUMN name VARCHAR(150);

-- Drop table
DROP TABLE Users;

-- Create index
CREATE INDEX idx_user_email ON Users(email);

-- Create view
CREATE VIEW ActiveUsers AS
SELECT * FROM Users WHERE status = 'ACTIVE';
```

### DML (Data Manipulation Language)
Used to manipulate data. Can be rolled back.

```sql
-- Insert data
INSERT INTO Users (name, email) VALUES ('John Doe', 'john@example.com');
INSERT INTO Users (name, email) VALUES
('Jane Smith', 'jane@example.com'),
('Bob Wilson', 'bob@example.com');

-- Update data
UPDATE Users SET name = 'John Smith' WHERE id = 1;

-- Delete data
DELETE FROM Users WHERE id = 1;

-- Select data
SELECT * FROM Users;
SELECT name, email FROM Users WHERE id = 1;
```

### DCL (Data Control Language)
Controls access to data.

```sql
-- Grant permissions
GRANT SELECT, INSERT ON Users TO 'app_user'@'localhost';
GRANT ALL PRIVILEGES ON mydb.* TO 'admin'@'%';

-- Revoke permissions
REVOKE INSERT ON Users FROM 'app_user'@'localhost';
```

### TCL (Transaction Control Language)
Manages transactions.

```sql
-- Start transaction
START TRANSACTION;

-- Commit changes
COMMIT;

-- Rollback changes
ROLLBACK;

-- Savepoint
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

### Interview Explanation:
"SQL commands are divided into four categories: DDL for structure (CREATE, ALTER, DROP), DML for data manipulation (SELECT, INSERT, UPDATE, DELETE), DCL for permissions (GRANT, REVOKE), and TCL for transactions (COMMIT, ROLLBACK). DDL commands are auto-committed and define the schema, while DML operations can be rolled back. In interviews, I emphasize that DDL changes structure permanently, while DML changes can be undone."

**Interview Tip:** DDL defines structure (auto-committed), DML manipulates data (rollback possible), DCL controls access, TCL manages transactions.

</details>

<details><summary>Aggregate Functions & GROUP BY</summary>

Aggregate functions perform calculations on groups of rows and return single values.

### Common Aggregate Functions:
```sql
-- Count rows
SELECT COUNT(*) FROM Users;
SELECT COUNT(DISTINCT department) FROM Employees;

-- Sum values
SELECT SUM(salary) FROM Employees;
SELECT SUM(salary) FROM Employees WHERE department = 'IT';

-- Average
SELECT AVG(salary) FROM Employees;

-- Minimum/Maximum
SELECT MIN(salary), MAX(salary) FROM Employees;

-- Grouped aggregates
SELECT department, COUNT(*), AVG(salary), SUM(salary)
FROM Employees
GROUP BY department;

-- With HAVING (filter groups)
SELECT department, AVG(salary), COUNT(*)
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY AVG(salary) DESC;
```

### GROUP BY with ROLLUP/CUBE:
```sql
-- ROLLUP: Hierarchical subtotals
SELECT department, job_title, SUM(salary)
FROM Employees
GROUP BY ROLLUP(department, job_title);

-- CUBE: All possible combinations
SELECT department, job_title, SUM(salary)
FROM Employees
GROUP BY CUBE(department, job_title);
```

### Interview Explanation:
"Aggregate functions like COUNT, SUM, AVG, MIN, MAX operate on groups of rows. GROUP BY creates these groups, and HAVING filters the groups (like WHERE for aggregates). For example, to find average salary by department, I use `SELECT department, AVG(salary) FROM Employees GROUP BY department`. I always mention that GROUP BY columns must appear in SELECT or be aggregated."

**Interview Tip:** GROUP BY creates groups, aggregate functions calculate per group. Use HAVING to filter groups, WHERE to filter rows.

</details>

<details><summary>Subqueries & Common Table Expressions (CTEs)</summary>

Subqueries are queries nested inside other queries. CTEs provide readable way to write complex queries.

### Subqueries:
```sql
-- Scalar subquery (returns single value)
SELECT name FROM Users
WHERE department_id = (SELECT id FROM Departments WHERE name = 'IT');

-- IN subquery (returns multiple values)
SELECT name FROM Users
WHERE id IN (SELECT user_id FROM Orders WHERE total > 1000);

-- EXISTS subquery (checks existence)
SELECT name FROM Users u
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.user_id = u.id);

-- Correlated subquery
SELECT name, (
    SELECT COUNT(*) FROM Orders
    WHERE Orders.user_id = Users.id
) as order_count
FROM Users;
```

### Common Table Expressions (CTEs):
```sql
-- Simple CTE
WITH HighValueOrders AS (
    SELECT * FROM Orders WHERE total > 1000
)
SELECT u.name, hvo.total
FROM Users u
JOIN HighValueOrders hvo ON u.id = hvo.user_id;

-- Recursive CTE (for hierarchical data)
WITH RECURSIVE EmployeeHierarchy AS (
    -- Base case
    SELECT id, name, manager_id, 0 as level
    FROM Employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive case
    SELECT e.id, e.name, e.manager_id, eh.level + 1
    FROM Employees e
    JOIN EmployeeHierarchy eh ON e.manager_id = eh.id
)
SELECT * FROM EmployeeHierarchy;
```

### Interview Explanation:
"Subqueries nest queries inside other queries - scalar for single values, IN for multiple values, EXISTS for existence checks. CTEs (WITH clauses) make complex queries readable by breaking them into logical parts. For example, I use CTEs for recursive queries like organizational hierarchies or complex aggregations. CTEs are more readable than subqueries and can be referenced multiple times."

**Interview Tip:** Use CTEs for complex queries, subqueries for simple cases. CTEs are more readable and can be recursive.

</details>

<details><summary>Views, Stored Procedures & Triggers</summary>

### Views:
Virtual tables based on SELECT queries. Simplify complex queries and provide security.

```sql
-- Create view
CREATE VIEW UserOrderSummary AS
SELECT
    u.name,
    u.email,
    COUNT(o.id) as total_orders,
    SUM(o.total) as total_spent,
    AVG(o.total) as avg_order_value
FROM Users u
LEFT JOIN Orders o ON u.id = o.user_id
GROUP BY u.id, u.name, u.email;

-- Use view
SELECT * FROM UserOrderSummary WHERE total_spent > 1000;

-- Updateable view (simple cases)
UPDATE UserOrderSummary SET name = 'John Smith' WHERE name = 'John Doe';
```

### Stored Procedures:
Precompiled SQL code stored in database. Improve performance and security.

```sql
DELIMITER //

CREATE PROCEDURE CreateUser(
    IN p_name VARCHAR(100),
    IN p_email VARCHAR(100),
    OUT p_user_id INT
)
BEGIN
    INSERT INTO Users (name, email, created_at)
    VALUES (p_name, p_email, NOW());

    SET p_user_id = LAST_INSERT_ID();
END //

DELIMITER ;

-- Call procedure
CALL CreateUser('Alice Johnson', 'alice@example.com', @user_id);
SELECT @user_id;
```

### Triggers:
Automatically execute when specific events occur (INSERT, UPDATE, DELETE).

```sql
-- Audit trigger
CREATE TRIGGER audit_user_changes
AFTER UPDATE ON Users
FOR EACH ROW
BEGIN
    INSERT INTO UserAudit (user_id, old_name, new_name, changed_at)
    VALUES (OLD.id, OLD.name, NEW.name, NOW());
END;

-- Prevent negative balance
CREATE TRIGGER check_balance
BEFORE UPDATE ON Accounts
FOR EACH ROW
BEGIN
    IF NEW.balance < 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Balance cannot be negative';
    END IF;
END;
```

### Interview Explanation:
"Views are virtual tables for simplifying queries and security. Stored procedures encapsulate business logic in the database, improving performance through precompilation and reducing network traffic. Triggers automatically enforce business rules or audit changes. I use views for complex joins, procedures for multi-step operations, and triggers for automatic auditing or constraint enforcement."

**Interview Tip:** Views for query simplification, procedures for business logic, triggers for automatic actions. Use carefully to avoid performance issues.

</details>

<details><summary>Database Constraints</summary>

Constraints enforce data integrity rules at database level.

### Types of Constraints:

#### Primary Key Constraint:
```sql
-- Single column
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- Composite primary key
CREATE TABLE OrderItems (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

#### Foreign Key Constraint:
```sql
CREATE TABLE Orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES Users(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

#### Unique Constraint:
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20)
);

-- Named constraint
ALTER TABLE Users ADD CONSTRAINT uk_user_phone UNIQUE (phone);
```

#### Check Constraint:
```sql
CREATE TABLE Products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2) CHECK (price > 0),
    stock INT CHECK (stock >= 0)
);

-- Age constraint
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18 AND age <= 120)
);
```

#### Not Null Constraint:
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);
```

### Interview Explanation:
"Constraints enforce data integrity: PRIMARY KEY for uniqueness and not null, FOREIGN KEY for relationships, UNIQUE for non-primary uniqueness, CHECK for business rules, NOT NULL for required fields. For example, I use CHECK constraints to ensure positive prices or valid age ranges. Foreign key constraints with CASCADE options automatically handle related data when parent records change."

**Interview Tip:** Use constraints for data integrity. Primary keys ensure uniqueness, foreign keys maintain relationships, check constraints enforce business rules.

</details>

<details><summary>Transactions & Isolation Levels</summary>

Transactions group multiple operations into single unit that either succeeds or fails completely.

### ACID Properties:
- **Atomicity**: All or nothing
- **Consistency**: Valid state transitions
- **Isolation**: Concurrent transactions don't interfere
- **Durability**: Changes persist after commit

### Transaction Commands:
```sql
-- Start transaction
START TRANSACTION;

-- Execute operations
UPDATE Accounts SET balance = balance - 100 WHERE id = 1;
UPDATE Accounts SET balance = balance + 100 WHERE id = 2;

-- Commit or rollback
COMMIT;    -- Save changes
ROLLBACK;  -- Undo changes
```

### Isolation Levels (SQL Standard):
```sql
-- Set isolation level
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

#### Isolation Level Comparison:
| Level | Dirty Read | Non-repeatable Read | Phantom Read | Performance |
|-------|------------|---------------------|--------------|-------------|
| Read Uncommitted | ✅ Possible | ✅ Possible | ✅ Possible | Fastest |
| Read Committed | ❌ Prevented | ✅ Possible | ✅ Possible | Fast |
| Repeatable Read | ❌ Prevented | ❌ Prevented | ✅ Possible | Medium |
| Serializable | ❌ Prevented | ❌ Prevented | ❌ Prevented | Slowest |

### Concurrency Problems:
- **Dirty Read**: Reading uncommitted changes
- **Non-repeatable Read**: Same row returns different values
- **Phantom Read**: New rows appear in subsequent reads

### Interview Explanation:
"Transactions ensure data consistency with ACID properties. Isolation levels control concurrency: Read Committed prevents dirty reads (most common), Repeatable Read prevents non-repeatable reads, Serializable prevents all anomalies but slowest. In banking, I use Serializable for transfers. In e-commerce, Read Committed balances consistency and performance."

**Interview Tip:** Use appropriate isolation levels. Read Committed is most common. Serializable prevents all anomalies but impacts performance.

</details>

<details><summary>Database Performance Tuning</summary>

Performance tuning involves optimizing queries, indexes, and database configuration for better speed.

### Query Optimization:
```sql
-- Bad: Full table scan
SELECT * FROM Users WHERE YEAR(created_at) = 2023;

-- Good: SARGable query
SELECT * FROM Users WHERE created_at >= '2023-01-01' AND created_at < '2024-01-01';

-- Use EXPLAIN to analyze
EXPLAIN SELECT * FROM Users WHERE email = 'john@example.com';
```

### Index Strategies:
```sql
-- Single column index
CREATE INDEX idx_users_email ON Users(email);

-- Composite index (order matters)
CREATE INDEX idx_orders_user_date ON Orders(user_id, order_date);

-- Partial index
CREATE INDEX idx_active_users ON Users(email) WHERE active = true;

-- Index for LIKE queries
CREATE INDEX idx_users_name ON Users(name varchar_pattern_ops);
```

### Query Optimization Techniques:
```sql
-- Use EXISTS instead of IN for large datasets
SELECT * FROM Users u
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.user_id = u.id);

-- Avoid SELECT *
SELECT id, name FROM Users WHERE active = true;

-- Use UNION ALL instead of UNION if duplicates not possible
SELECT name FROM Customers UNION ALL SELECT name FROM Suppliers;

-- Optimize JOINs
SELECT u.name, COUNT(o.id)
FROM Users u
LEFT JOIN Orders o ON u.id = o.user_id
WHERE u.created_at > '2023-01-01'
GROUP BY u.id, u.name;
```

### Database Configuration:
- **Connection Pooling**: Reuse connections (HikariCP)
- **Query Caching**: Cache frequent queries
- **Partitioning**: Split large tables
- **Replication**: Read replicas for scaling

### Interview Explanation:
"Performance tuning starts with EXPLAIN plans to identify slow queries. I add indexes on WHERE and JOIN columns, avoid full table scans, and use appropriate data types. For example, I replace `LIKE '%text%'` with full-text search, and use composite indexes for multi-column WHERE clauses. I also consider partitioning for large tables and read replicas for high-traffic applications."

**Interview Tip:** Use EXPLAIN to analyze queries. Index WHERE/JOIN columns. Avoid SELECT *, use appropriate data types, consider partitioning.

</details>

<details><summary>Database Design Patterns</summary>

Common patterns for scalable, maintainable database design.

### 1. Audit Trail Pattern:
Track all changes to data for compliance and debugging.

```sql
-- Audit table
CREATE TABLE UserAudit (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    action VARCHAR(10), -- INSERT, UPDATE, DELETE
    old_values JSON,
    new_values JSON,
    changed_by INT,
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Trigger to populate audit
CREATE TRIGGER audit_users AFTER UPDATE ON Users
FOR EACH ROW
INSERT INTO UserAudit (user_id, action, old_values, new_values)
VALUES (NEW.id, 'UPDATE', JSON_OBJECT('name', OLD.name), JSON_OBJECT('name', NEW.name));
```

### 2. Soft Delete Pattern:
Mark records as deleted instead of physically removing them.

```sql
ALTER TABLE Users ADD COLUMN deleted_at TIMESTAMP NULL;
CREATE INDEX idx_users_deleted ON Users(deleted_at);

-- Soft delete
UPDATE Users SET deleted_at = NOW() WHERE id = 1;

-- Query active records
SELECT * FROM Users WHERE deleted_at IS NULL;
```

### 3. Polymorphic Associations:
Single table references multiple parent tables.

```sql
-- Comments table for multiple entities
CREATE TABLE Comments (
    id INT PRIMARY KEY,
    content TEXT,
    entity_type VARCHAR(50), -- 'post', 'product', 'user'
    entity_id INT,          -- ID in respective table
    user_id INT,
    created_at TIMESTAMP
);

-- Query comments for a post
SELECT * FROM Comments
WHERE entity_type = 'post' AND entity_id = 123;
```

### 4. Data Warehousing (Star Schema):
Optimized for analytics and reporting.

```sql
-- Fact table
CREATE TABLE SalesFacts (
    id INT PRIMARY KEY,
    product_id INT,
    customer_id INT,
    store_id INT,
    sale_date DATE,
    quantity INT,
    amount DECIMAL(10,2)
);

-- Dimension tables
CREATE TABLE DimProducts (id INT PRIMARY KEY, name VARCHAR(100), category VARCHAR(50));
CREATE TABLE DimCustomers (id INT PRIMARY KEY, name VARCHAR(100), region VARCHAR(50));
CREATE TABLE DimStores (id INT PRIMARY KEY, name VARCHAR(100), location VARCHAR(100));
```

### Interview Explanation:
"Database design patterns solve common problems: Audit trails for tracking changes, soft deletes for data recovery, polymorphic associations for flexible relationships, and star schemas for analytics. I choose patterns based on requirements - audit trails for compliance, soft deletes for user-facing apps, star schemas for reporting systems."

**Interview Tip:** Use audit trails for compliance, soft deletes for user data, star schema for analytics. Choose patterns based on specific requirements.

</details>

<details><summary>Indexing</summary>

Indexing improves database query performance by creating a fast lookup structure that allows the database to find rows efficiently without scanning the entire table.

Types: B-Tree, Hash, Bitmap.

Example:
```sql
CREATE INDEX idx_user_name ON Users(name);
```

**Interview Tip:** Index speeds SELECT, slows INSERT/UPDATE. Use for frequently queried columns.

</details>

<details><summary>Joins: INNER, LEFT, RIGHT</summary>

SQL JOINs are used to combine rows from two or more tables based on a related column.

### INNER JOIN
Returns only matching records from both tables.

Example:
```sql
SELECT u.name, o.amount
FROM Users u
INNER JOIN Orders o ON u.user_id = o.user_id;
```

### LEFT JOIN (LEFT OUTER JOIN)
Returns all records from the left table and matching records from the right table. If no match → NULL.

Example:
```sql
SELECT u.name, o.amount
FROM Users u
LEFT JOIN Orders o ON u.user_id = o.user_id;
```

### RIGHT JOIN (RIGHT OUTER JOIN)
Returns all records from the right table and matching records from the left table. If no match → NULL.

Example:
```sql
SELECT u.name, o.amount
FROM Users u
RIGHT JOIN Orders o ON u.user_id = o.user_id;
```

**Interview Tip:** INNER for matching rows, LEFT for all left + matching right.

</details>

<details><summary>ACID Properties</summary>

ACID properties ensure reliable database transactions by guaranteeing atomicity, consistency, isolation, and durability.

| Property    | Meaning |
|-------------|---------|
| Atomicity  | All or nothing |
| Consistency | Valid state before & after |
| Isolation  | Transactions run independently |
| Durability | Data persists after commit |

### Atomicity
All or nothing
- Either the whole transaction completes
- Or the database rolls back completely
Example: If money is deducted but not credited → rollback ❌

### Consistency
Database moves from one valid state to another
- Rules, constraints, keys must be preserved
- No data corruption
Example: Balance can't go negative if constraint exists.

### Isolation
Transactions don't interfere with each other
- Concurrent transactions behave as if executed one by one
Isolation problems:
- Dirty Read
- Non-repeatable Read
- Phantom Read
Isolation levels control this.

### Durability
Once committed, data stays committed
- Even if system crashes
- Data is safely stored on disk/logs

**Interview Tip:** ACID ensures data reliability. NoSQL sacrifices some for scalability.

</details>

<details><summary>Optimizing Slow Queries</summary>

Slow queries are optimized by analyzing execution plans, using proper indexes, minimizing data retrieval, optimizing joins, and applying caching where appropriate.

Identify slow query: Run EXPLAIN ANALYZE, Add/fix indexes, Rewrite query, Cache if needed.

Example EXPLAIN:
```sql
EXPLAIN SELECT * FROM Users WHERE name = 'John';
```

**Interview Tip:** Use EXPLAIN to analyze query plans. Index WHERE clauses.

</details>

## REST API Design

<details><summary>Idempotency</summary>

Idempotency ensures that repeated execution of an operation produces the same result as a single execution, preventing duplicate side effects in distributed systems.

Idempotent operation = safe to repeat without side effects.

Example: PUT request - updating a resource multiple times gives same result.

**Interview Tip:** Use idempotency keys for payments, updates.

</details>

<details><summary>Pagination</summary>

Pagination means fetching data in chunks (pages) instead of loading everything at once.
- Improve performance
- Reduce memory usage
- Handle large datasets

Pagination in Java is implemented using Pageable to fetch data in chunks, while sorting is applied using Sort to order results based on specified fields.

Example Spring Data:
```java
Page<User> users = userRepository.findAll(PageRequest.of(0, 10, Sort.by("name")));
```

**Interview Tip:** Use offset/limit or cursor-based pagination.

</details>

<details><summary>API Versioning</summary>

API versioning is the practice of managing API changes by maintaining multiple versions to ensure backward compatibility for existing clients.

Methods: URI versioning (v1/users), Header versioning, Query param versioning.

Real-World Example:
- v1 → returns name
- v2 → returns firstName, lastName
Old clients still work using v1.

Example:
```java
@GetMapping("/v1/users")
public List<UserV1> getUsersV1() { ... }

@GetMapping("/v2/users")
public List<UserV2> getUsersV2() { ... }
```

**Interview Tip:** Version APIs to avoid breaking changes.

</details>

<details><summary>Request/Response DTOs</summary>

Request/Response DTOs (Data Transfer Objects) are simple objects used to carry data between the client and server, without exposing internal domain models.

Request and Response DTOs are used to transfer data between the client and server while keeping APIs decoupled from internal domain models.

Example Request DTO:
```java
class CreateUserRequest {
    @NotNull
    private String name;
    @Email
    private String email;
}
```

Example Response DTO:
```java
class UserResponse {
    private Long id;
    private String name;
    private String email;
}
```

**Interview Tip:** DTOs hide internal models, add validation, and control data exposure.

</details>

<details><summary>Interview Questions</summary>

<details><summary>What is database normalization and why is it important?</summary>

**Explanation:** Normalization organizes data to reduce redundancy and improve integrity by splitting tables based on dependencies.

**Example:** Separate Customer and Order tables instead of repeating customer info in every order.

**Real-time Example:** In an e-commerce database, normalization prevents updating customer address in multiple places when it changes.

</details>

<details><summary>Explain ACID properties with examples.</summary>

**Explanation:** ACID ensures reliable transactions: Atomicity (all or nothing), Consistency (valid states), Isolation (independent transactions), Durability (persists after commit).

**Example:** Bank transfer: Deduct from account A and add to B atomically; if failure, rollback both.

**Real-time Example:** Online banking ensures money transfers are durable even if server crashes after commit.

</details>

<details><summary>What are SQL JOINs and when to use each type?</summary>

**Explanation:** JOINs combine data from multiple tables. INNER returns matching rows, LEFT includes all left + matches, RIGHT all right + matches.

**Example:** INNER JOIN users and orders on user_id to get users with orders.

**Real-time Example:** In a blog, LEFT JOIN posts and comments to show posts even without comments.

</details>

<details><summary>How do you optimize slow database queries?</summary>

**Explanation:** Use indexes on WHERE columns, analyze EXPLAIN plans, avoid SELECT *, limit data with pagination.

**Example:** Add index on email column for fast user lookups.

**Real-time Example:** In a search engine, indexing keywords speeds up queries from seconds to milliseconds.

</details>

<details><summary>What is the difference between SQL and NoSQL databases?</summary>

**Explanation:** SQL is relational with fixed schema, NoSQL is flexible for unstructured data, better for scalability.

**Example:** SQL for banking (strict consistency), NoSQL for social media (flexible posts).

**Real-time Example:** MongoDB for storing varied product catalogs in e-commerce vs PostgreSQL for financial records.

</details>

<details><summary>Explain database normalization and its importance.</summary>

**Explanation:** Normalization organizes data to reduce redundancy and anomalies by splitting tables based on dependencies.

**Example:** Separate Customer and Order tables instead of repeating customer info in every order.

**Real-time Example:** In an e-commerce database, normalization prevents updating customer address in multiple places when it changes.

</details>

<details><summary>What are database transactions and why are they important?</summary>

**Explanation:** Transactions group operations that must succeed or fail together, ensuring data consistency.

**Example:** Bank transfer: deduct from account A and credit to B must both succeed or both rollback.

**Real-time Example:** In online shopping, order placement involves inventory reduction and payment processing as one transaction.

</details>

<details><summary>Explain the concept of database indexing.</summary>

**Explanation:** Indexes speed up data retrieval by creating sorted data structures, but slow down writes.

**Example:** B-tree index on email column allows fast user lookups by email.

**Real-time Example:** In a user login system, indexing email speeds up authentication from O(n) to O(log n).

</details>

<details><summary>What are the different types of database relationships?</summary>

**Explanation:** One-to-one, one-to-many, many-to-many relationships define how tables connect.

**Example:** User has one profile (one-to-one), user has many orders (one-to-many), students enroll in many courses (many-to-many).

**Real-time Example:** In a blog system, author has many posts (one-to-many), posts have many tags (many-to-many).

</details>

</details>