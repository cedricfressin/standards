## API endpoint standards and conventions

### API Design

- **RESTful Design**: Follow REST principles with clear resource-based URLs and appropriate HTTP methods (GET, POST, PUT, PATCH, DELETE)
- **Consistent Naming**: Use consistent, lowercase, hyphenated or underscored naming conventions for endpoints across the API
- **Versioning**: Implement API versioning strategy (URL path or headers) to manage breaking changes without disrupting existing clients
- **Plural Nouns**: Use plural nouns for resource endpoints (e.g., `/users`, `/products`) for consistency
- **Nested Resources**: Limit nesting depth to 2-3 levels maximum to keep URLs readable and maintainable
- **Query Parameters**: Use query parameters for filtering, sorting, pagination, and search rather than creating separate endpoints
- **HTTP Status Codes**: Return appropriate, consistent HTTP status codes (200, 201, 400, 404, 500, etc.) accompanied by structured error bodies for better client handling

### Authentication & Authorization

- **Authentication**: Implement proper authentication flows utilizing secure protocols like JWT or OAuth, combined with HTTPS, to handle user sessions and API access securely. Verify JWTs on every request and implement appropriate session expiration
- **Authorization**: Use role-based access control (RBAC) enforced in both the application and database layers

### Input Validation & Security

- **Input Validation**: Always validate client inputs using type-safe schemas like Zod and sanitize user-generated content with DOMPurify
- **Security Measures**: Employ parameterized queries to prevent SQL injection, validate and scan file uploads for type, size, and malware
- **Secrets Management**: Never expose sensitive data in client code, including API keys, secrets, and any confidential information; load all sensitive information from environment variables without hardcoding any secrets

### Network Security

- **CORS Configuration**: Explicitly configure and validate Cross-Origin Resource Sharing to control access from different origins
- **HTTPS Enforcement**: Use HTTPS for all network requests; enforce HTTPS in production for all communications, including API calls, to encrypt data in transit and ensure secure connections
- **Certificate Pinning**: Implement certificate pinning for API calls; pin expected certificates to prevent man-in-the-middle attacks during secure API communications

### Attack Prevention

- **Rate Limiting**: Implement rate limiting for API routes by applying configurable per-user and per-IP rate limits to prevent abuse, brute-force attacks, and denial-of-service scenarios, and include rate limit information in response headers to help clients manage their usage
- **CSRF Protection**: Use CSRF protection for mutations; implement anti-CSRF tokens or equivalent mechanisms to safeguard state-changing requests from cross-site request forgery
- **Content Security Policy**: Use Content Security Policy headers; configure CSP headers to define allowed content sources, thereby reducing the risk of XSS, inline script execution, and data injection attacks

### Compliance & Monitoring

- **Auditing**: Log all sensitive operations to maintain an audit trail for security and compliance
