# Roadmap

Рабочая структура книги `Backend Engineer Handbook`.

Подзаголовок:

> Понимание технологий через путешествие одного запроса.

## Принцип структуры

Книга строится не как набор независимых определений, а как последовательное понимание backend-системы:

```text
Пользовательский запрос
  ↓
Сеть / HTTP
  ↓
Входной слой
  ↓
ASP.NET Core
  ↓
Бизнес-логика
  ↓
Данные
  ↓
Интеграции
  ↓
Наблюдаемость
  ↓
Доставка в production
```

Новые темы добавляются туда, где они естественно отвечают на инженерный вопрос.

---

## Часть I. Путешествие одного запроса

Цель — не изучать сети как Network Engineer, а понять минимальный фундамент, который нужен .NET Backend-разработчику.

1. URL
2. DNS
3. IP-адрес
4. Port
5. TCP
6. TLS
7. HTTP
8. HTTPS
9. Полное путешествие запроса

Статус: черновик модуля написан полностью.

---

## Часть II. Входной слой приложения

1. Kestrel
2. Nginx
3. Reverse Proxy
4. Load Balancer
5. API Gateway
6. YARP / альтернативы Nginx в .NET-экосистеме
7. Docker Networking для backend-разработчика
8. WebSocket / Polling / Long Polling
9. gRPC

Комментарий: `gRPC` лучше рассматривать после HTTP/Kestrel/Nginx, когда уже понятно, как сервисы принимают запросы и почему REST не всегда удобен для service-to-service communication.

---

## Часть III. ASP.NET Core

1. ASP.NET Core Pipeline
2. Middleware
3. Routing
4. Controllers vs Minimal API
5. Filters
6. Model Binding
7. Validation
8. ProblemDetails
9. Dependency Injection
10. Configuration / Options Pattern
11. Logging
12. Hosted Services / BackgroundService
13. Health Checks
14. Authentication
15. Authorization
16. Claims / Permissions / Policies
17. API Versioning
18. Swagger / OpenAPI
19. Rate Limiting

---

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

---

## Часть V. Данные и базы данных

1. SQL база для backend-разработчика
2. PostgreSQL
3. MS SQL Server
4. PostgreSQL vs MS SQL для .NET Backend
5. EF Core
6. Dapper
7. Transactions
8. Isolation Levels
9. MVCC
10. Locks / FOR UPDATE / NOWAIT
11. Deadlocks
12. Indexes
13. B-Tree
14. GIN
15. GiST
16. ltree
17. Recursive CTE
18. JSONB / JSON в разных СУБД
19. Execution Plan / EXPLAIN ANALYZE
20. VACUUM / ANALYZE
21. Normal Forms / Denormalization
22. Read Replica
23. Optimistic vs Pessimistic Locking

Комментарий: `MS SQL Server` не выносится как изолированная большая книга. Основной практический формат — сравнение `PostgreSQL vs MS SQL` с акцентом на .NET backend, EF Core, индексы, транзакции, JSON, identity/sequence, locking и типичные вопросы собеседований.

---

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
18. Feature Flags / Feature Toggles
19. Distributed Transactions: почему обычно избегают

---

## Часть VII. Интеграции и distributed systems

1. REST как базовый способ общения сервисов
2. gRPC
3. RabbitMQ
4. Kafka
5. Kafka vs RabbitMQ
6. Outbox Pattern
7. Inbox Pattern
8. Retry / Dead Letter Queue
9. Exactly once vs at least once
10. Saga
11. Redis
12. Memory Cache vs Distributed Cache
13. HybridCache
14. Distributed Locks
15. Quartz.NET
16. Polly: Retry / Timeout / Circuit Breaker / Fallback

Комментарий: `Kafka` лучше изучать через сравнение с `RabbitMQ`, а не как отдельную абстрактную технологию. Главный вопрос: когда нужна очередь команд/сообщений, а когда нужен event streaming/log.

---

## Часть VIII. Observability

1. Что такое Observability
2. Logs / Metrics / Traces
3. Structured Logging
4. Serilog
5. Seq
6. Prometheus
7. Grafana
8. Loki
9. Tempo
10. OpenTelemetry
11. Correlation ID / Trace ID
12. Health Checks vs Metrics
13. Alerting
14. Observability в ASP.NET Core

Комментарий: эта часть должна объяснять не инструменты сами по себе, а путь диагностики production-системы: от логов к метрикам, от метрик к трейсам, от трейсов к полной картине запроса.

---

## Часть IX. Storage и файлы

1. S3 / MinIO
2. Pre-signed URLs
3. Multipart Upload
4. HLS / Video Processing
5. FileService reliability

---

## Часть X. Docker и окружение

1. Docker basics для backend-разработчика
2. Dockerfile
3. Docker Compose
4. Volumes
5. Networks
6. Healthcheck
7. Environment variables
8. Secrets в local/dev окружении

---

## Часть XI. CI/CD и доставка

1. Что такое CI
2. Что такое CD
3. Pipeline
4. Build
5. Tests
6. Docker build
7. Deploy
8. Rollback
9. GitHub Actions
10. Jenkins
11. TeamCity / Azure DevOps обзорно
12. CI/CD для .NET backend

Комментарий: `Jenkins` рассматривается внутри общей главы CI/CD. На собеседованиях важнее понимать pipeline и lifecycle доставки, чем знать только один инструмент.

---

## Часть XII. Kubernetes для backend-разработчика

Без DevOps-глубины. Цель — понимать, что происходит с backend-приложением в Kubernetes.

1. Pod
2. Deployment
3. Service
4. Ingress
5. ConfigMap
6. Secret
7. Rolling Update
8. HPA
9. Logs / Metrics в Kubernetes

---

## Часть XIII. Практика проектов

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
12. Observability stack в проекте
13. AuthService architecture после завершения реализации

---

## Приоритет ближайших модулей

1. Завершить review Модуля I: `Путешествие одного запроса`
2. ASP.NET Core Request Pipeline
3. Kestrel
4. Nginx / Reverse Proxy
5. Docker Networking
6. Auth / JWT / Claims / Policy
7. async/await + ThreadPool
8. SemaphoreSlim + Task.WhenAll
9. PostgreSQL Locks / FOR UPDATE
10. RabbitMQ / Outbox
11. gRPC
12. Kafka vs RabbitMQ
13. Observability stack
14. CI/CD
15. PostgreSQL vs MS SQL
