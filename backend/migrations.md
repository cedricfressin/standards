## Database migration best practices

### Migration Design

- **Reversible Migrations**: Always implement rollback/down methods to enable safe migration reversals
- **Small, Focused Changes**: Keep each migration focused on a single logical change for clarity and easier troubleshooting
- **Separate Schema and Data**: Keep schema changes separate from data migrations for better rollback safety
- **Naming Conventions**: Use clear, descriptive names that indicate what the migration does

### Version Control

- **Version Control and Immutability**: Always commit all migration files to version control and never modify existing or applied migrations after deployment or production release; create new migrations for corrections instead

### Performance & Safety

- **Zero-Downtime Deployments**: Consider deployment order and backwards compatibility for high-availability systems
- **Index Management**: Create indexes on large tables carefully, using concurrent options when available to avoid locks
- **Testing Protocol**: Test migrations thoroughly on a staging environment before deploying to production

### Prisma-Specific

- **Prisma Workflow**: Baseline existing databases with `prisma db pull`; use Prisma for schema changes and manual SQL for RLS policies and triggers
- **Direct Connections**: Always use the direct database connection (DIRECT_URL) for migrations to bypass connection pooling
- **Deployment Commands**: Use `prisma migrate deploy` for production and `prisma migrate status` to verify application

### Security & Access Control

- **RLS Integration**: Enable Row Level Security and define CRUD policies immediately after creating tables in migrations
