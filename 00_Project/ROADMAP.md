# Roadmap

Рабочая структура книги `Backend Engineer Handbook`.

## Часть I. Сетевой фундамент для Backend

Эта часть должна быть краткой. Цель — не изучать сети как DevOps/Network Engineer, а понимать термины, которые будут встречаться в следующих главах.

1. DNS
2. TCP
3. UDP
4. HTTP
5. HTTPS / TLS
6. HTTP/2 и HTTP/3
7. WebSocket / Polling / Long Polling
8. gRPC

## Часть II. Входной слой приложения

1. Kestrel
2. Nginx
3. Reverse Proxy
4. Load Balancer
5. API Gateway
6. YARP / альтернативы Nginx в .NET-экосистеме
7. Docker Networking для backend-разработчика

## Часть III. ASP.NET Core

1. ASP.NET Core Pipeline
2. Middleware
3. Routing
4. Controllers vs Minimal API
5. Dependency Injection
6. Configuration / Options Pattern
7. Logging
8. Hosted Services / BackgroundService
9. Health Checks
10. Authentication
11. Authorization
12. Claims / Permissions / Policies

## Часть IV. C# и CLR

1. CLR / JIT / AOT
2. Value Types vs Reference Types
3. Stack / Heap / RAM
4. Boxing / Unboxing
5. GC
6. LOH
7. Workstation GC vs Server GC
8. Thread / ThreadPool
9. async/await
10. Task / ValueTask
11. Task.WhenAll
12. CancellationToken
13. SynchronizationContext / ConfigureAwait
14. lock / Monitor / Interlocked / SemaphoreSlim
15. Concurrent Collections
16. Closures
17. Delegates / Events
18. LINQ
19. IEnumerable vs IQueryable
20. Expression Tree
21. Pattern Matching
22. Records / Immutability
23. Nullable Reference Types
24. Attributes

## Часть V. PostgreSQL и базы данных

1. SQL база для backend-разработчика
2. Transactions
3. Isolation Levels
4. MVCC
5. Locks / FOR UPDATE / NOWAIT
6. Deadlocks
7. Indexes
8. B-Tree
9. GIN
10. GiST
11. ltree
12. Recursive CTE
13. JSONB
14. Execution Plan / EXPLAIN ANALYZE
15. VACUUM / ANALYZE
16. Normal Forms / Denormalization
17. Read Replica
18. Optimistic vs Pessimistic Locking

## Часть VI. Архитектура

1. Monolith
2. Modular Monolith
3. Microservices
4. Clean Architecture
5. DDD
6. Entity / Value Object / Aggregate
7. Domain Events
8. CQRS
9. Repository
10. Unit of Work
11. MediatR
12. GRASP
13. SOLID
14. Coupling / Cohesion
15. CAP Theorem
16. Idempotency
17. Event-Driven Architecture

## Часть VII. Distributed Systems

1. RabbitMQ
2. Kafka
3. Outbox Pattern
4. Inbox Pattern
5. Retry / Dead Letter Queue
6. Exactly once vs at least once
7. Saga
8. Redis
9. Memory Cache vs Distributed Cache
10. HybridCache
11. Rate Limiting
12. Distributed Locks
13. Quartz.NET
14. Observability
15. OpenTelemetry / Metrics / Logs / Traces

## Часть VIII. Storage и файлы

1. S3 / MinIO
2. Pre-signed URLs
3. Multipart Upload
4. HLS / Video Processing
5. FileService reliability

## Часть IX. Практика проектов

1. DirectoryService
2. FileService
3. AuthService
4. Video Processing Pipeline
5. Integration Tests
6. Docker Compose окружение
7. Nginx в проекте
8. PostgreSQL locks в DepartmentRepository
9. SemaphoreSlim + Task.WhenAll в FileService
10. Quartz jobs в FileService
11. RabbitMQ / events / statuses

## Первая рабочая глава

- `02_Entry_Layer/02_Nginx.md`

## Приоритет ближайших глав

1. Nginx
2. Kestrel
3. HTTP кратко
4. Docker Networking
5. ASP.NET Core Pipeline
6. Auth / JWT / Claims / Policy
7. async/await + ThreadPool
8. SemaphoreSlim + Task.WhenAll
9. PostgreSQL Locks / FOR UPDATE
10. RabbitMQ / Outbox
