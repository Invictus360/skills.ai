---
name: api-design-rest
description: When creating or extending an HTTP API for client consumption.
version: 1.0.0
tags: [backend, api, rest]
---

# RESTful API Design

## When to use
- Building a new backend service exposing resources.
- Adding a new domain entity to an existing API.
- Creating integration endpoints for third-party partners.

## What it does
Provides a predictable, resource-oriented architecture for HTTP APIs, making them intuitive for consumers and standardizing request/response payloads.

## Workflow
1. **Identify Resources**: Map business entities to Plural Nouns (e.g., `users`, `invoices`).
2. **Assign Verbs**: Map CRUD operations to correct HTTP methods (GET, POST, PUT, PATCH, DELETE).
3. **Design URL Hierarchy**: Nest resources logically but no deeper than two levels (e.g., `/users/{id}/orders`).
4. **Standardize Responses**: Wrap success payloads in a consistent envelope (optional) and error responses in an RFC 7807 problem details object.
5. **Add Pagination**: For collection endpoints, mandate `limit` and `offset` (or cursors) from day one.

## Rules
- Use HTTP status codes semantically (200, 201, 400, 401, 403, 404, 500).
- URLs must be entirely lowercase, using hyphens for multiple words.
- APIs must be versioned (e.g., via URL `/v1/` or headers).

## Anti-patterns
- **Verbs in URLs**: Creating endpoints like `/getUsers` or `/updateOrder`.
- **200 OK Errors**: Returning HTTP 200 for a failed business logic transaction.
- **Deep Nesting**: Endpoints like `/companies/{id}/departments/{id}/employees/{id}/tasks`.

## Output format
An OpenAPI/Swagger schema definition or a structured router file implementing standard HTTP methods for a pluralized noun path.
