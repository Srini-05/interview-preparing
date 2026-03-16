# Database

## Normalization

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity by dividing data into related tables.

### Normal Forms
- 1NF: Eliminate repeating groups
- 2NF: Remove partial dependencies
- 3NF: Remove transitive dependencies

Example: Unnormalized table with redundancy → Normalized into Customer, Order, Product tables.

**Interview Tip:** Normalization reduces data duplication and anomalies.

## Primary key vs Foreign key

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

## Indexing

Indexing improves database query performance by creating a fast lookup structure that allows the database to find rows efficiently without scanning the entire table.

Types: B-Tree, Hash, Bitmap.

Example:
```sql
CREATE INDEX idx_user_name ON Users(name);
```

**Interview Tip:** Index speeds SELECT, slows INSERT/UPDATE. Use for frequently queried columns.

## Joins: INNER, LEFT, RIGHT

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

## ACID Properties

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

## Optimizing Slow Queries

Slow queries are optimized by analyzing execution plans, using proper indexes, minimizing data retrieval, optimizing joins, and applying caching where appropriate.

Identify slow query: Run EXPLAIN ANALYZE, Add/fix indexes, Rewrite query, Cache if needed.

Example EXPLAIN:
```sql
EXPLAIN SELECT * FROM Users WHERE name = 'John';
```

**Interview Tip:** Use EXPLAIN to analyze query plans. Index WHERE clauses.

## REST API Design

## Idempotency

Idempotency ensures that repeated execution of an operation produces the same result as a single execution, preventing duplicate side effects in distributed systems.

Idempotent operation = safe to repeat without side effects.

Example: PUT request - updating a resource multiple times gives same result.

**Interview Tip:** Use idempotency keys for payments, updates.

## Pagination

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

## API Versioning

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

## Request/Response DTOs

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