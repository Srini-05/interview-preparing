# Database

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>`.

<details><summary>Normalization</summary>

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity by dividing data into related tables.

### Normal Forms
- 1NF: Eliminate repeating groups
- 2NF: Remove partial dependencies
- 3NF: Remove transitive dependencies

Example: Unnormalized table with redundancy → Normalized into Customer, Order, Product tables.

**Interview Tip:** Normalization reduces data duplication and anomalies.

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

</details>