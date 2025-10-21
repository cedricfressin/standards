## Database query best practices

### Security

- **Prevent SQL Injection**: Always use parameterized queries or ORM methods like Prisma's prepared statements; never interpolate user input into SQL strings

### Performance Optimization

- **Avoid N+1 Queries**: Use eager loading or joins to fetch related data in a single query instead of multiple queries
- **Select Only Needed Data**: Request only the columns you need rather than using `SELECT *` for better performance
- **Index Strategic Columns**: Index columns used in WHERE, JOIN, and ORDER BY clauses for query optimization
- **Set Query Timeouts**: Implement timeouts to prevent runaway queries from impacting system performance
- **Bulk Operations**: Leverage Prisma's `createMany` and `updateMany` methods for efficient batch inserts and updates
- **Cursor Pagination**: Use cursor-based pagination for large datasets to improve performance over offset methods

### Transaction Management

- **Use Transactions for Related Changes**: Wrap related database operations in transactions to maintain data consistency

### Caching

- **Caching**: Cache results of complex, expensive, or frequently-run queries using Redis with short TTLs (1–5m) and invalidation on writes when appropriate

### Monitoring

- **Query Optimization**: Analyze slow queries with PostgreSQL's `EXPLAIN ANALYZE` and monitor via `pg_stat_statements`
