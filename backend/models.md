## Database model best practices

### Naming Conventions

- **Naming Conventions**: Use singular names for models, plural for tables in `snake_case` following PostgreSQL and framework conventions

### Schema Design

- **Timestamps**: Include `created_at` and `updated_at` as `TIMESTAMPTZ` on all tables for auditing, debugging, and proper timezone handling
- **UUID Primary Keys**: Implement primary keys as UUID v4 with `DEFAULT gen_random_uuid()`
- **Appropriate Data Types**: Choose data types that match the data's purpose and size requirements

### Data Integrity

- **Data Integrity**: Use database constraints (NOT NULL, UNIQUE, foreign keys, CHECK) to enforce data rules and business invariants at the database level
- **Relationship Clarity**: Define relationships clearly with appropriate cascade behaviors and naming conventions
- **Validation at Multiple Layers**: Implement validation at both model and database levels for defense in depth

### Indexing & Performance

- **Indexing**: Index foreign key columns, frequently queried fields, and apply partial unique indexes for soft-delete scenarios or GIN for full-text search

### Normalization

- **Normalization**: Target at least 3NF, balance normalization with practical query performance needs, avoid storing derived values, and use junction tables for many-to-many relationships

### Special Features

- **Soft Deletes**: Add `deleted_at TIMESTAMPTZ` nullable column for soft deletion when data retention is required
- **RLS Enablement**: Enable Row Level Security on tables that require user or tenant data isolation
