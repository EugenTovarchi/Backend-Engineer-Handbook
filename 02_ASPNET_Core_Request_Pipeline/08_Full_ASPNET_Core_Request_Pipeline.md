# Модуль II. ASP.NET Core Request Pipeline: от Kestrel до Endpoint

# Глава 8. Полный ASP.NET Core Request Pipeline

──────────────────────────────────────────────

**МОДУЛЬ II • ASP.NET Core Request Pipeline**

**Прогресс до главы:** 88% (7 из 8 глав завершены)

**Маршрут:** Kestrel → HttpContext → Middleware → Routing → Authentication → Authorization → Endpoint → Full Pipeline

**Текущая глава:** Full Pipeline

**Текущий вопрос:**  
Как все этапы складываются в одну реальную обработку запроса?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

## Зачем нужна эта глава

Мы разобрали части ASP.NET Core request pipeline по отдельности:

- [Kestrel](./01_Kestrel_ASPNET_Core_Boundary.md);
- [HttpContext](./02_HttpContext.md);
- [Middleware](./03_Middleware_Pipeline.md);
- [Routing](./04_Routing_Endpoint_Selection.md);
- [Authentication](./05_Authentication_In_Pipeline.md);
- [Authorization](./06_Authorization_In_Pipeline.md);
- [Endpoint](./07_Endpoint_Execution.md).

Теперь нужно собрать их в одну рабочую модель.

Важно: маршрут модуля — учебная модель, а не обещание, что любой request всегда проходит каждый этап.

---

## Короткое определение

**ASP.NET Core Request Pipeline (конвейер обработки запроса — последовательность компонентов, через которые проходит `HttpContext`)** описывает путь запроса внутри .NET-приложения.

Pipeline может ветвиться, завершаться досрочно и выполнять разные типы endpoint.

ASP.NET Core Hosting — инфраструктура размещения и запуска ASP.NET Core, которая находится между веб-сервером и pipeline приложения.

---

## Полная схема

```mermaid
sequenceDiagram
    participant Client as Client
    participant Kestrel as Kestrel
    participant Hosting as ASP.NET Core Hosting
    participant Context as HttpContext
    participant M1 as Exception/Logging Middleware
    participant Routing as Routing
    participant AuthN as Authentication
    participant AuthZ as Authorization
    participant Endpoint as Endpoint

    Client->>Kestrel: HTTP request
    Kestrel->>Hosting: pass request data
    Hosting->>Context: create HttpContext
    Context->>M1: enter middleware
    M1->>Routing: await next()
    Routing->>Routing: select endpoint
    Routing->>AuthN: await next()
    AuthN->>AuthN: set HttpContext.User
    AuthN->>AuthZ: await next()
    AuthZ->>AuthZ: check endpoint metadata
    AuthZ->>Endpoint: await next()
    Endpoint-->>AuthZ: результат / HTTP-ответ
    AuthZ-->>AuthN: HTTP-ответ возвращается
    AuthN-->>Routing: HTTP-ответ возвращается
    Routing-->>M1: HTTP-ответ возвращается
    M1-->>Kestrel: HTTP-ответ возвращается
    Kestrel-->>Client: HTTP-ответ
```

---

## Последовательный пример

Запрос:

```text
GET /api/files/123
Authorization: Bearer <token>
```

Учебная цепочка:

```text
Kestrel
  ↓
HttpContext
  ↓
Logging middleware
  ↓
Routing
  ↓
Authentication
  ↓
Authorization
  ↓
GET /api/files/{id}
  ↓
Обработчик endpoint
  ↓
200 OK / 401 / 403 / 404 / 405 / 500
```

---

## Пример Program.cs

```csharp
using System.Diagnostics;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddProblemDetails();
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer");

builder.Services.AddAuthorization();

var app = builder.Build();

app.UseExceptionHandler();

app.Use(async (context, next) =>
{
    var startedAt = Stopwatch.GetTimestamp();

    try
    {
        await next(context);
    }
    finally
    {
        var elapsed = Stopwatch.GetElapsedTime(startedAt);
        Console.WriteLine(
            $"{context.Request.Path} -> {context.Response.StatusCode} за {elapsed.TotalMilliseconds} ms");
    }
});

app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();

app.MapGet("/api/files/{id}", (string id) =>
{
    return Results.Ok(new { Id = id });
}).RequireAuthorization();

app.MapGet("/health", () => Results.Ok("Healthy"))
    .AllowAnonymous();

app.Run();
```

Пример показывает порядок, но не означает, что каждый request обязан пройти одинаковый путь. Явный `UseRouting()` показывает место сопоставления endpoint. В современном `WebApplication` routing и middleware выполнения endpoint могут добавляться инфраструктурой ASP.NET Core автоматически; `MapGet` регистрирует endpoint, а инфраструктура ASP.NET Core добавляет выполнение endpoint в pipeline. Например, `/health` может разрешать анонимный доступ, а exception middleware может обработать ошибку раньше ответа клиенту.

---

## Обратное движение HTTP-ответа

Запрос идёт внутрь через middleware.

HTTP-ответ возвращается наружу через те middleware, которые вызвали `next`.

Если middleware завершил request досрочно и не вызвал `next`, компоненты глубже не выполняются.

Пример:

```text
Middleware A вызывает next
  Middleware B записывает HTTP-ответ без next
Middleware A получает HTTP-ответ обратно
```

Endpoint в этом сценарии не выполняется.

---

## Сценарии досрочного завершения

Request может завершиться до endpoint:

| Сценарий | Пример результата |
|---|---|
| Статические файлы найдены | `200 OK` без controller |
| Endpoint разрешает анонимный доступ | authorization не требует аутентифицированного пользователя |
| Пользовательский middleware вернул ошибку | `400 Bad Request` |
| Routing не нашёл endpoint | `404 Not Found` |
| Путь существует, но HTTP-метод не поддерживается | `405 Method Not Allowed` |
| Защищённый endpoint без аутентифицированного пользователя | authorization запускает challenge, обработчик Bearer-схемы обычно формирует `401` |
| Аутентифицированный пользователь без нужных прав | authorization запускает forbid, обработчик Bearer-схемы обычно формирует `403` |
| Обработчик исключений обработал ошибку | `500` или ProblemDetails |

---

## Диагностика по слоям

| Симптом | Где смотреть сначала | Возможная причина |
|---|---|---|
| `404` | Routing | путь не сопоставился |
| `405` | Routing / сопоставление HTTP-метода | путь существует, HTTP-метод не поддерживается |
| `401` | Authorization challenge / схема аутентификации | защищённый endpoint, личность пользователя не установлена |
| `403` | Authorization forbid | личность пользователя есть, требования доступа не выполнены |
| `500` | Middleware / Endpoint | необработанное exception |
| request не дошёл до приложения | входной слой / Kestrel | неверный порт, прокси-сервер, размещение и запуск приложения, проблема соединения |

Инфраструктурная ошибка до Kestrel отличается от ошибки внутри pipeline приложения: если request не дошёл до ASP.NET Core, middleware и endpoint не выполнялись.

---

## Важные оговорки

Не каждый request проходит:

```text
Authentication → Authorization → Controller
```

Причины:

- middleware может завершить request досрочно;
- pipeline может ветвиться через `Map`;
- endpoint может разрешать анонимный доступ;
- статические файлы и endpoint проверки состояния приложения могут обрабатываться по более короткому пути;
- controller action не является обязательным типом endpoint;
- HTTP-ответ возвращается только через middleware, которые вызвали `next`.

Статические файлы могут быть возвращены middleware или endpoint без controller action.

Health check быстро возвращает состояние приложения для мониторинга, балансировщика или оркестратора.

---

## Что происходит дальше

Теперь понятно, где authentication и authorization находятся внутри ASP.NET Core request pipeline.

Но это ещё не полная authentication-система.

Следующий модуль разбирает отдельную инженерную историю:

```text
Identity
Credentials
JWT
Access Token
Refresh Token
Claims / Roles / Permissions / Policies
OAuth 2.0
OpenID Connect
ASP.NET Core Identity
AuthService
```

То есть Модуль III посвящён аутентификации и авторизации как полноценной системе.

---

## Вопросы собеседования

### Junior: Что такое ASP.NET Core request pipeline?

<details>
<summary>Ответ</summary>

Это последовательность компонентов, через которые проходит `HttpContext`: middleware, routing, authentication, authorization и endpoint execution. Pipeline может завершить request раньше endpoint.

</details>

---

### Middle: Почему порядок middleware важен?

<details>
<summary>Ответ</summary>

Потому что каждый middleware видит context в текущем состоянии. Например, authorization должен видеть выбранный endpoint и установленного пользователя, поэтому routing и authentication обычно идут раньше.

</details>

---

### Middle: Чем filters отличаются от middleware?

<details>
<summary>Ответ</summary>

Middleware работает на уровне всего ASP.NET Core pipeline и может обработать request ещё до routing или endpoint. Filters выполняются ближе к MVC/action или endpoint execution и применяются к выбранному механизму обработки. Поэтому filters не заменяют middleware, а решают другую задачу внутри более позднего этапа.

</details>

---

### Senior: Почему endpoint может не выполниться?

<details>
<summary>Ответ</summary>

Endpoint может не выполниться, если middleware завершил request досрочно, routing не нашёл endpoint, сопоставление HTTP-метода вернуло `405`, authorization инициировал challenge/forbid или произошла ошибка раньше выполнения endpoint.

</details>

---

### Architect / System Design: Как диагностировать проблему в request pipeline?

<details>
<summary>Ответ</summary>

Нужно идти по слоям: сначала понять, дошёл ли request до ASP.NET Core, затем проверить middleware, routing, authentication, authorization и выполнение endpoint. `404` чаще связан с сопоставлением пути, `405` — с сопоставлением HTTP-метода, `401` — с authorization challenge и схемой аутентификации, `403` — с authorization forbid, `500` — с exception в middleware или прикладной логике. Такой подход отделяет инфраструктурные проблемы от проблем внутри pipeline приложения.

</details>

---

## Ответ для собеседования

ASP.NET Core request pipeline — это цепочка обработки `HttpContext` после того, как request попал в приложение через Kestrel и инфраструктура размещения и запуска ASP.NET Core создала контекст запроса. Обычно request проходит через middleware, routing выбирает endpoint, authentication пытается установить `HttpContext.User`, authorization проверяет доступ по endpoint metadata, а затем выполняется endpoint: controller action, обработчик Minimal API, health check или другой обработчик. Если защищённый endpoint требует пользователя, но личность пользователя не установлена, authorization инициирует challenge, а обработчик Bearer-схемы обычно возвращает `401`. Важно помнить, что это не жёсткая обязательная цепочка для любого запроса: middleware может завершить request досрочно, pipeline может ветвиться, endpoint может разрешать анонимный доступ, а controller не является обязательным элементом. HTTP-ответ возвращается наружу через middleware, которые вызвали `next`.

---

## Итоговая шпаргалка

- Kestrel передаёт request в ASP.NET Core.
- `HttpContext` хранит состояние текущего запроса.
- Middleware образуют pipeline.
- `next` передаёт request дальше.
- HTTP-ответ возвращается через middleware обратно.
- Routing выбирает endpoint.
- Authentication пытается установить пользователя по предоставленным учётным данным.
- Authorization проверяет доступ.
- Endpoint выполняет обработчик или метод controller action.
- Request может завершиться до endpoint.
- `404`, `405`, `401`, `403`, `500` диагностируются по разным слоям.
- `401` для Bearer API обычно появляется через authorization challenge.
- Полная auth-система будет в Модуле III.

---

## Прогресс модуля

**Модуль II:** `ASP.NET Core Request Pipeline`  
**Прогресс после главы:** 100% (8 из 8 глав завершены).
