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

Эта схема показывает архитектурные слои production-системы, а не обязательный порядок изучения модулей. В книге ASP.NET Core Request Pipeline рассматривается раньше Production Entry Layer, потому что он является прямым продолжением финала Модуля I.

Новые темы добавляются туда, где они естественно отвечают на инженерный вопрос.

---

## Модуль I. Путешествие одного запроса

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

Статус: написан полностью, первый редакторский проход завершён, ожидает финального review пользователем.

---

## Модуль II. ASP.NET Core Request Pipeline

Цель — понять, что происходит после того, как HTTP-запрос достиг .NET-приложения: от границы Kestrel до выполнения endpoint.

1. Граница Kestrel и ASP.NET Core
2. HttpContext
3. Middleware Pipeline
4. Routing и выбор Endpoint
5. Authentication внутри Pipeline
6. Authorization внутри Pipeline
7. Выполнение Endpoint
8. Полный ASP.NET Core Request Pipeline

Комментарий: Authentication и Authorization в Модуле II рассматриваются как этапы ASP.NET Core Request Pipeline. Полное устройство authentication-системы, JWT, refresh token, OAuth 2.0, OpenID Connect, ASP.NET Core Identity, хранение пользователей и AuthService рассматриваются в отдельном Модуле III.

---

## Модуль III. Аутентификация и авторизация

Предварительный маршрут:

1. Identity, Authentication и Authorization
2. Credentials и хранение пользователей
3. Authentication в ASP.NET Core
4. JWT
5. Access Token
6. Refresh Token
7. Claims, Roles, Permissions и Policies
8. OAuth 2.0
9. OpenID Connect
10. ASP.NET Core Identity
11. Архитектура AuthService
12. Полный путь аутентификации

---

## Модуль IV. Production Entry Layer

Цель — разобрать production-вход перед ASP.NET Core приложением в контексте входящего запроса.

1. Kestrel как production web server
2. Nginx
3. Reverse Proxy
4. Load Balancer
5. API Gateway
6. YARP
7. Forwarded Headers
8. TLS termination на proxy
9. Docker Networking в пути от proxy до приложения

Комментарий: WebSocket, Polling, Long Polling и gRPC не входят в обязательную цепочку Production Entry Layer. Они относятся к способам взаимодействия и интеграциям и рассматриваются в будущих разделах отдельно.

---

## Модуль V. ASP.NET Core Web API и инфраструктура приложения

Цель — разобрать, как ASP.NET Core превращает выбранный endpoint в полноценный Web API: получает входные данные, проверяет их, вызывает application code, формирует стандартный HTTP response и предоставляет инфраструктуру приложения.

Предварительный состав:

1. Controllers vs Minimal APIs
2. MVC и endpoint execution model
3. Filters и Endpoint Filters
4. Model Binding
5. Validation
6. ProblemDetails и обработка ошибок API
7. Dependency Injection
8. Service Lifetimes: Transient, Scoped, Singleton
9. Configuration и Options Pattern
10. Logging в ASP.NET Core
11. Hosted Services / BackgroundService
12. Health Checks
13. API Versioning
14. Swagger / OpenAPI
15. Rate Limiting

Review: CORS найден в пользовательских конспектах и остаётся кандидатом для Модуля V до утверждения структуры этого модуля.

---

## Часть VI. C# и CLR

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

## Часть VII. Данные и базы данных

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

## Часть VIII. Архитектура

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

## Часть IX. Интеграции и distributed systems

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

## Часть X. Observability

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

## Часть XI. Storage и файлы

1. S3 / MinIO
2. Pre-signed URLs
3. Multipart Upload
4. HLS / Video Processing
5. FileService reliability

---

## Часть XII. Docker и окружение

1. Docker basics для backend-разработчика
2. Dockerfile
3. Docker Compose
4. Volumes
5. Networks
6. Healthcheck
7. Environment variables
8. Secrets в local/dev окружении

---

## Часть XIII. CI/CD и доставка

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

## Часть XIV. Kubernetes для backend-разработчика

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

## Часть XV. Практика проектов

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
2. Модуль II — ASP.NET Core Request Pipeline
3. Модуль III — Аутентификация и авторизация
4. Модуль IV — Production Entry Layer
5. Модуль V — ASP.NET Core Web API и инфраструктура приложения
6. async/await + ThreadPool
7. SemaphoreSlim + Task.WhenAll
8. PostgreSQL Locks / FOR UPDATE
9. RabbitMQ / Outbox
10. gRPC
11. Kafka vs RabbitMQ
12. Observability stack
13. CI/CD
14. PostgreSQL vs MS SQL
