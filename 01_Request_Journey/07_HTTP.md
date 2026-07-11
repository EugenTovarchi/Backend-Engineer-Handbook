# Модуль I. Путешествие одного запроса

# Глава 7. HTTP

──────────────────────────────────────────────

**МОДУЛЬ I • Путешествие одного запроса**

**Прогресс до главы:** 67% (6 из 9 глав завершены)

**Маршрут:** URL → DNS → IP → Port → TCP → TLS → HTTP → HTTPS → Full Journey
**Текущая глава:** HTTP

**Текущий вопрос:**  
В каком формате клиент и сервер будут обмениваться запросами и ответами?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

## Исходная ситуация

У браузера уже есть:

```text
✓ URL
✓ IP-адрес
✓ Port
✓ TCP-соединение
✓ защищённый канал TLS, если используется HTTPS
```

Теперь можно передавать данные.

Но клиент и сервер должны договориться не только о том, как передавать байты, но и о том, что эти байты означают.

Нужен общий язык общения.

Для Web API таким языком обычно является HTTP.

---

## Зачем нужна эта глава

HTTP — центральный протокол для ASP.NET Core Web API.

Он напрямую связан с:

| Где | Как связан HTTP |
|---|---|
| Controllers / Minimal API | endpoint получает HTTP request |
| Middleware | работает с HTTP context |
| Authentication | читает headers/cookies |
| Authorization | принимает решение по request context |
| Swagger/OpenAPI | описывает HTTP API |
| Nginx | проксирует HTTP-запросы |
| REST | строится поверх HTTP |
| GraphQL | обычно работает через HTTP endpoint |
| WebSocket | часто начинается как HTTP Upgrade |

Если не понимать HTTP, трудно уверенно говорить про ASP.NET Core pipeline, status codes, headers, body, cookies, JWT, CORS и обратный прокси.

---

## Эта глава понадобится позже

- [HTTPS](./08_HTTPS.md)
- [Kestrel](../02_Entry_Layer/01_Kestrel.md)
- [ASP.NET Core Pipeline](../03_ASPNET_Core/01_ASPNET_Core_Pipeline.md)
- [Middleware](../03_ASPNET_Core/02_Middleware.md)
- [Routing](../03_ASPNET_Core/03_Routing.md)
- [Controllers](../03_ASPNET_Core/04_Controllers_vs_Minimal_API.md)
- [Minimal API](../03_ASPNET_Core/04_Controllers_vs_Minimal_API.md)
- [Authentication](../03_ASPNET_Core/14_Authentication.md)
- [Authorization](../03_ASPNET_Core/15_Authorization.md)
- [CORS](../03_ASPNET_Core/01_ASPNET_Core_Pipeline.md)
- [REST](../07_Integrations/01_REST.md)
- [GraphQL](../07_Integrations/01_REST.md)

---

## Короткое определение

**HTTP (HyperText Transfer Protocol — протокол передачи гипертекста)** — это прикладной протокол request/response для обмена данными между клиентом и сервером.

Упрощённо:

```text
Client отправляет HTTP request.
Server возвращает HTTP response.
```

HTTP определяет структуру сообщения: method, path, headers, body, status code.

---

## Простое объяснение

Представь форму обращения в службу поддержки.

В ней есть:

- тип обращения;
- адрес отдела;
- дополнительные поля;
- текст сообщения.

HTTP request похож на такую форму.

Например:

```http
GET /api/files/123 HTTP/1.1
Host: company.com
Authorization: Bearer <token>
Accept: application/json
```

Сервер читает request и возвращает response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": "123",
  "name": "video.mp4"
}
```

---

## HTTP request

HTTP request обычно содержит:

```text
Method
Path
Headers
Body
```

Пример:

```http
POST /api/files HTTP/1.1
Host: company.com
Content-Type: application/json
Authorization: Bearer <token>

{
  "name": "video.mp4"
}
```

Разберём части.

---

## Method

**Method (метод HTTP — часть запроса, которая показывает намерение клиента)** показывает, что клиент хочет сделать.

Частые методы:

| Method | Обычно означает |
|---|---|
| `GET` | получить данные |
| `POST` | создать ресурс или выполнить команду |
| `PUT` | заменить ресурс целиком |
| `PATCH` | частично изменить ресурс |
| `DELETE` | удалить ресурс |
| `OPTIONS` | служебный запрос, часто для CORS |

Важно: HTTP method — это соглашение. Реальное поведение зависит от backend-кода.

Но на собеседовании ожидают понимания общих семантик.

---

## Path

Path (путь) указывает, к какому ресурсу или endpoint обращается клиент.

Примеры:

```text
/api/files/123
/api/departments/roots
/api/auth/login
```

В ASP.NET Core path участвует в routing.

Например:

```csharp
[HttpGet("api/files/{id:guid}")]
public async Task<IActionResult> GetFile(Guid id)
{
    ...
}
```

---

## Headers

**Headers (заголовки)** — это metadata запроса или ответа.

Примеры request headers:

```http
Authorization: Bearer <token>
Content-Type: application/json
Accept: application/json
User-Agent: Mozilla/5.0
```

Headers используются для:

- authentication;
- content negotiation;
- CORS;
- cookies;
- caching;
- tracing;
- forwarded headers за обратным прокси.

---

## Body

**Body (тело запроса/ответа)** содержит полезные данные.

Например JSON:

```json
{
  "email": "user@example.com",
  "password": "secret"
}
```

Обычно:

- `GET` чаще не имеет body;
- `POST`, `PUT`, `PATCH` часто имеют body;
- response body содержит результат, ошибку или данные.

---

## HTTP response

HTTP response обычно содержит:

```text
Status code
Headers
Body
```

Пример:

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": "123"
}
```

---

## Status codes

**Status code (код состояния)** показывает результат обработки запроса.

Группы:

| Код | Группа | Смысл |
|---:|---|---|
| `2xx` | Success | успешно |
| `3xx` | Redirection | перенаправление |
| `4xx` | Client error | ошибка клиента |
| `5xx` | Server error | ошибка сервера |

Частые коды:

| Код | Значение |
|---:|---|
| `200 OK` | успешно |
| `201 Created` | создано |
| `204 No Content` | успешно, без body |
| `400 Bad Request` | некорректный запрос |
| `401 Unauthorized` | пользователь не аутентифицирован |
| `403 Forbidden` | нет прав |
| `404 Not Found` | ресурс не найден |
| `409 Conflict` | конфликт состояния |
| `500 Internal Server Error` | ошибка сервера |
| `502 Bad Gateway` | обратный прокси не смог корректно получить ответ от backend-сервиса |

---

## HTTP в ASP.NET Core

В ASP.NET Core HTTP request попадает в pipeline.

Упрощённо:

```text
Kestrel
  ↓
HttpContext
  ↓
Middleware
  ↓
Routing
  ↓
Endpoint
  ↓
Response
```

`HttpContext` содержит:

- request;
- response;
- user;
- headers;
- route values;
- cancellation token;
- connection info.

Практически весь ASP.NET Core pipeline работает вокруг HTTP context.

---

## HTTP и REST

REST API часто использует HTTP methods и status codes как часть контракта.

Например:

```text
GET    /api/files/123      -> получить файл
POST   /api/files          -> создать файл
DELETE /api/files/123      -> удалить файл
```

Но REST — это архитектурный стиль, а HTTP — протокол.

Они связаны, но это не одно и то же.

---

## HTTP и GraphQL

GraphQL тоже часто работает поверх HTTP.

Например:

```text
POST /graphql
```

Тело запроса содержит GraphQL query.

То есть GraphQL не заменяет HTTP. Он обычно использует HTTP как транспорт для запросов.

---

## Практика из проекта

В сервисах вроде DirectoryService, FileService и AuthService внешний контракт обычно выражается через HTTP API.

Например:

```text
GET /api/departments/roots
POST /api/files/uploads/init
POST /api/auth/login
```

Nginx может принять внешний запрос:

```text
/directory-service/api/departments/roots
```

переписать path и передать в ASP.NET Core:

```text
/api/departments/roots
```

Дальше ASP.NET Core Routing выбирает endpoint, а middleware могут проверить authentication, authorization, logging, exception handling и т.д.

---

## Типичные ошибки

### Ошибка 1. Путать HTTP и TCP

TCP отвечает за соединение и доставку байтов.

HTTP отвечает за формат request/response.

---

### Ошибка 2. Путать `401` и `403`

`401 Unauthorized` — пользователь не аутентифицирован.

`403 Forbidden` — пользователь известен, но у него нет прав.

---

### Ошибка 3. Использовать `GET` для операций с изменением состояния

По семантике `GET` должен быть безопасным и не менять состояние системы.

Для команд обычно используют `POST`, `PUT`, `PATCH`, `DELETE`.

---

### Ошибка 4. Всегда возвращать `200 OK`

HTTP status codes — часть API-контракта.

Если всё возвращать как `200`, клиенту сложнее корректно обрабатывать ошибки.

---

## Что происходит дальше

Теперь понятно, что HTTP задаёт формат общения клиента и сервера.

Но в современном интернете HTTP почти всегда передаётся через TLS.

То есть на практике мы чаще используем HTTPS.

Следующая глава собирает это вместе:

```text
HTTP + TLS = HTTPS
```

---

## Вопросы собеседования

### Junior: Что такое HTTP?

<details>
<summary>Ответ</summary>

HTTP — это прикладной протокол request/response. Клиент отправляет request, сервер возвращает response. HTTP определяет methods, path, headers, body и status codes.

</details>

---

### Middle: Чем HTTP отличается от TCP?

<details>
<summary>Ответ</summary>

TCP — транспортный протокол, который устанавливает соединение и передаёт байты. HTTP — прикладной протокол, который задаёт формат request/response поверх транспорта.

</details>

---

### Middle: Чем `401` отличается от `403`?

<details>
<summary>Ответ</summary>

`401 Unauthorized` означает, что пользователь не аутентифицирован или не предоставил валидные credentials. `403 Forbidden` означает, что пользователь известен, но у него нет прав на действие или ресурс.

</details>

---

### Senior: Почему status codes являются частью API-контракта?

<details>
<summary>Ответ</summary>

Потому что клиент использует status code для принятия решений: повторить запрос, показать ошибку, перенаправить пользователя, обновить токен или обработать конфликт. Если backend всегда возвращает `200 OK`, клиент теряет стандартный механизм интерпретации результата.

</details>

---

## Ответ для собеседования

HTTP — это прикладной протокол request/response, на котором строятся Web API. Он определяет структуру запроса и ответа: method, path, headers, body и status code. В ASP.NET Core HTTP request проходит через Kestrel и pipeline, где middleware, routing и endpoint обрабатывают его через `HttpContext`. Важно отличать HTTP от TCP: TCP отвечает за соединение и доставку байтов, а HTTP — за смысл этих байтов. Для backend-разработчика HTTP важен как внешний контракт API: методы, статусы, заголовки, body, authentication, CORS, cookies и взаимодействие с обратным прокси.

---

## Шпаргалка

- HTTP — протокол request/response.
- Request содержит method, path, headers, body.
- Response содержит status code, headers, body.
- HTTP работает поверх транспорта, обычно TCP.
- HTTPS = HTTP поверх TLS.
- `401` — не аутентифицирован.
- `403` — нет прав.
- Status codes — часть API-контракта.
- ASP.NET Core работает с HTTP через `HttpContext`.
- REST и GraphQL часто используют HTTP, но не являются самим HTTP.

---

## Прогресс модуля

**Модуль I:** `Путешествие одного запроса`  
**Прогресс после главы:** 78% (7 из 9 глав завершены).
