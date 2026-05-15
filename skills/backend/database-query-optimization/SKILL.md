---
name: database-query-optimization
description: When addressing slow application endpoints, high database CPU usage, or standardizing data access patterns.
version: 1.0.0
tags: [backend, database, performance, sql]
---

# Database Query Optimization

## When to use
- Writing complex SQL queries or ORM access functions.
- Resolving performance bottlenecks on read-heavy endpoints.
- Designing schema migrations for growing datasets.

## What it does
Reduces database load and network latency by eliminating inefficient access patterns, leveraging indexes correctly, and ensuring the database does the heavy lifting rather than the application code.

## Workflow
1. **Analyze Execution**: Use `EXPLAIN` or `EXPLAIN ANALYZE` on slow queries to identify sequential scans and high-cost operations.
2. **Eliminate N+1**: Identify loops making repetitive database calls. Replace them with single `IN (...)` queries or ORM eager-loading (e.g., `JOIN`).
3. **Selectivity**: Replace `SELECT *` with explicit column names to reduce memory allocation and network payload size.
4. **Index Optimization**: Add B-Tree indexes to columns frequently used in `WHERE`, `JOIN`, and `ORDER BY` clauses. 
5. **Paginate**: Never query unbounded datasets. Enforce `LIMIT` and `OFFSET` (or cursor-based pagination) at the query level.

## Rules
- Explicitly define selected columns (never use `SELECT *` in production).
- Database operations inside iterative loops (e.g., `for`, `map`) are strictly forbidden.
- Filtering and aggregating must happen in the database, not in the application memory.

## Anti-patterns
- **The N+1 Problem**: Fetching a list of 50 users, then making 50 individual queries to fetch each user's profile.
- **Over-indexing**: Adding an index to every single column, which degrades `INSERT` and `UPDATE` performance.
- **Application-Side Filtering**: Fetching 10,000 rows from the DB and using `Array.prototype.filter()` in JavaScript to find 10 specific records.

## Output format
Optimized raw SQL queries or configured ORM methods accompanied by a database migration script for any necessary indexes.

## Example (optional)

**❌ Anti-pattern (ORM N+1 & Over-fetching):**
```javascript
// Fetches ALL columns, creates N+1 queries
const users = await User.findAll(); 
for (const user of users) {
  const posts = await Post.find({ userId: user.id });
  console.log(user, posts);
}
```
**✅ Hardened Pattern (Optimized):**
```javascript
// Explicit columns, single query with JOIN/Eager Loading
const usersWithPosts = await User.findAll({
  attributes: ['id', 'username'],
  include: [{
    model: Post,
    attributes: ['id', 'title'],
    required: true
  }]
```
});
