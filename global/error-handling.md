## Error handling best practices

### Error Detection & Handling

- **Fail Fast and Explicitly**: Validate input and check preconditions early; fail with clear error messages rather than allowing invalid state
- **Specific Exception Types**: Use specific exception/error types rather than generic ones to enable targeted handling
- **Centralized Error Handling**: Handle errors at appropriate boundaries (controllers, API layers) rather than scattering try-catch blocks everywhere
- **Clean Up Resources**: Always clean up resources (file handles, connections) in finally blocks or equivalent mechanisms
- **Type-Safe Throwing**: Throw `Error` instances (not strings); include meaningful messages; avoid swallowing errors or empty catch blocks

### User Experience

- **User-Friendly Messages**: Provide clear, actionable error messages to users without exposing technical details or security information
- **Preserve User Input and Context**: Keep form data and page state on error; allow easy retry without data loss
- **Actionable Recovery**: Provide clear next steps (retry, back, contact/help) and suggest corrections when possible
- **Internationalization**: Localize error messages and hints; keep them concise and actionable

### System Resilience

- **Graceful Degradation**: Design systems to degrade gracefully when non-critical services fail rather than breaking entirely
- **Retry Strategies**: Implement exponential backoff for transient failures in external service calls
- **Graceful Degradation & Offline**: Show fallback UI when dependencies fail; queue or no-op non-critical actions when offline (mobile)

### Implementation Best Practices

- **Domain-Level Errors**: Wrap low-level/ORM/database errors into domain errors; never leak internal messages or stack traces to clients

### Monitoring

- **Observability & Monitoring**: Capture exceptions in reporting services with safe context (user/session/correlation-id) and redact sensitive data
