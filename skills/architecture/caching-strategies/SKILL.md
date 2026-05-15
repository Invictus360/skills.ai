---
name: caching-strategies
description: When improving read performance and reducing database load.
version: 1.0.0
tags: [architecture, performance, caching]
---

# Caching Strategies

## When to use
- System is experiencing high latency on read-heavy API endpoints.
- Database CPU/Memory usage is constantly peaking due to repeated queries.
- Designing a new system expecting massive read throughput.

## What it does
Stores copies of frequently accessed data in a fast, temporary storage layer (like Redis or Memcached) to intercept requests before they hit the primary database.

## Workflow
1. **Identify Bottlenecks**: Profile APIs to find read-heavy, slow-changing data (e.g., user profiles, static config, product catalogs).
2. **Select Strategy**:
    - *Cache-Aside*: App checks cache; on miss, fetches from DB, writes to cache.
    - *Write-Through*: App writes to cache and DB simultaneously.
3. **Set Eviction Policy**: Assign Time-To-Live (TTL) values based on business tolerance for stale data.
4. **Handle Invalidation**: Implement cache invalidation logic on mutations (UPDATE/DELETE) for the relevant resources.
5. **Avoid Stampedes**: Implement caching locks or staggered TTLs to prevent multiple clients fetching from the DB simultaneously when a key expires.

## Rules
- Cache must always be treated as ephemeral (can disappear at any time).
- Do not cache highly personalized or sensitive data (like PII) in shared edge caches.
- Always implement a fallback to the primary data store on cache failure.

## Anti-patterns
- **Infinite TTL**: Storing keys without an expiration, leading to unbounded memory growth and stale data.
- **Premature Caching**: Adding Redis to an architecture before verifying the database is properly indexed.

## Output format
Implementation of a cache-aside wrapper function integrating an in-memory datastore with fallback database retrieval.
