---
name: logging-observability-standards
description: When setting up telemetry, debugging distributed systems, or standardizing application output.
version: 1.0.0
tags: [architecture, observability, logging, backend]
---

# Logging & Observability Standards

## When to use
- Bootstrapping a new backend microservice or monolithic API.
- Refactoring code filled with disorganized `console.log` or `print` statements.
- Designing a system that spans multiple services/functions.

## What it does
Ensures application state and failures are highly searchable, machine-readable, and traceable across system boundaries without leaking sensitive user data.

## Workflow
1. **Implement Structured Logging**: Configure the logger to output NDJSON (Newline Delimited JSON) instead of plain text strings.
2. **Inject Context**: Attach a `correlation_id` (or `trace_id`) at the HTTP entry point and pass it through all downstream functions and service calls.
3. **Standardize Levels**: 
   - `ERROR`: System is broken/failing (requires alerts).
   - `WARN`: Unexpected state, but system recovered.
   - `INFO`: Significant lifecycle events (Server started, User registered).
   - `DEBUG`: Verbose logic tracing (disabled in production).
4. **Sanitize Data**: Implement a redaction middleware to mask credentials, tokens, and PII (Personally Identifiable Information) before it hits the log stream.

## Rules
- Logs must be formatted as JSON in production environments.
- Every HTTP request must generate a unique Request ID/Correlation ID.
- Never log raw passwords, session tokens, or financial data.

## Anti-patterns
- **String Concatenation**: `logger.info("User " + userId + " failed to login")` (Prevents easy querying. Use JSON properties instead).
- **Logging Expected Errors as ERROR**: Logging an `ERROR` when a user types the wrong password (this is expected business logic, use `INFO` or `WARN`).
- **Silent Catching**: Catching an exception without logging the stack trace and context.

## Output format
A configured logger instance (e.g., Winston, Pino, Serilog) and a middleware function that injects trace IDs and automatically logs request/response metadata.
