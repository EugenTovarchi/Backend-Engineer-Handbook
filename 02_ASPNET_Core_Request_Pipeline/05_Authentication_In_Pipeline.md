# Модуль II. ASP.NET Core Request Pipeline: от Kestrel до Endpoint

# Глава 5. Authentication внутри Pipeline

──────────────────────────────────────────────

**МОДУЛЬ II • ASP.NET Core Request Pipeline**

**Прогресс до главы:** 50% (4 из 8 глав завершены)

**Маршрут:** Kestrel → HttpContext → Middleware → Routing → Authentication → Authorization → Endpoint → Full Pipeline
**Текущая глава:** Authentication

**Текущий вопрос:**  
Как pipeline устанавливает, кто отправил запрос?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

## Исходная ситуация

[Routing](./04_Routing_Endpoint_Selection.md) может выбрать endpoint.

Но перед проверкой доступа приложению нужно понять:

> Кто отправил request?

Этим занимается authentication.

---

## Зачем нужна эта глава

Authentication в pipeline объясняет:

- откуда появляется `HttpContext.User`;
- почему возможен `401 Unauthorized`;
- зачем нужен `UseAuthentication`;
- почему bearer token и cookie являются credentials;
- почему authentication не равна authorization.

Полное устройство JWT, refresh token, OAuth 2.0, OpenID Connect, ASP.NET Core Identity и AuthService будет в Модуле III.

---

## Эта глава понадобится позже

- [Authorization внутри Pipeline](./06_Authorization_In_Pipeline.md)
- [Выполнение Endpoint](./07_Endpoint_Execution.md)
- [Полный ASP.NET Core Request Pipeline](./08_Full_ASPNET_Core_Request_Pipeline.md)
- Аутентификация и авторизация в будущем Модуле III

---

## Короткое определение

**Authentication (аутентификация — процесс установления личности отправителя запроса)** проверяет credentials и заполняет `HttpContext.User`.

**Credentials (учётные данные — данные, по которым можно попытаться установить пользователя)** могут быть bearer token, cookie, API key или другие данные.

Authentication отвечает на вопрос:

```text
Кто отправил request?
```

---

## Простая аналогия

Authentication похожа на проверку паспорта.

Охрана смотрит документ и говорит:

```text
Это Иван.
```

Но сама проверка паспорта ещё не отвечает, можно ли Ивану войти в конкретную комнату. Это уже authorization.

---

## Техническое объяснение

В ASP.NET Core authentication обычно подключается так:

```csharp
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", options =>
    {
        options.Authority = "https://auth.example";
        options.Audience = "files-api";
    });

var app = builder.Build();

app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
```

Здесь:

- authentication scheme определяет способ проверки;
- handler выполняет проверку credentials;
- результат записывается в `HttpContext.User`.

**Authentication scheme (схема аутентификации — именованный способ проверки credentials)** может быть `Bearer`, `Cookies` или другой вариант.

---

## ClaimsIdentity и ClaimsPrincipal

**ClaimsIdentity (идентичность с claims — набор утверждений о пользователе и признак authenticated)** описывает одну identity.

**ClaimsPrincipal (представление пользователя — объект, который может содержать одну или несколько identities)** хранится в `HttpContext.User`.

Упрощённо:

```text
Bearer token / Cookie
  ↓
Authentication handler
  ↓
ClaimsPrincipal
  ↓
HttpContext.User
```

Если credentials невалидны или отсутствуют, user может остаться unauthenticated.

---

## Authenticate, challenge и 401

Authenticate (проверка credentials — попытка установить пользователя) выполняется authentication handler-ом.

Если endpoint требует пользователя, а он не установлен, приложение может вернуть challenge.

**Challenge (запрос аутентификации — ответ, который сообщает клиенту, что нужно предоставить валидные credentials)** часто приводит к:

```text
401 Unauthorized
```

Название `Unauthorized` исторически сбивает с толку: чаще оно означает именно отсутствие валидной authentication.

---

## Bearer token и cookie

Bearer token:

```http
Authorization: Bearer <access_token>
```

Cookie:

```http
Cookie: sessionId=abc
```

Оба варианта могут быть credentials.

В этой главе они нужны только как примеры данных, по которым pipeline устанавливает пользователя. Их полное устройство относится к Модулю III.

---

## Схема

```mermaid
sequenceDiagram
    participant C as Client
    participant A as Authentication Middleware
    participant H as Authentication Handler
    participant X as HttpContext

    C->>A: request with credentials
    A->>H: authenticate
    H-->>A: ClaimsPrincipal or no result
    A->>X: set HttpContext.User
```

---

## Типичные ошибки

Ошибка: путать authentication и authorization.  
Почему неверно: authentication устанавливает пользователя, authorization проверяет доступ.  
Как правильно: разделять вопросы `кто это` и `что ему разрешено`.

Ошибка: ждать от authentication проверки прав.  
Почему неверно: права проверяются на этапе authorization.  
Как правильно: authentication должна подготовить `HttpContext.User`.

Ошибка: раскрывать JWT полностью в pipeline-главе.  
Почему неверно: это отдельная инженерная история.  
Как правильно: здесь объяснить место bearer token в pipeline, а детали вынести в Модуль III.

---

## Вопросы собеседования

### Junior: Что делает authentication?

<details>
<summary>Ответ</summary>

Authentication проверяет credentials и устанавливает пользователя в `HttpContext.User`.

</details>

---

### Middle: Что такое authentication scheme?

<details>
<summary>Ответ</summary>

Authentication scheme — это именованный способ аутентификации, например `Bearer` или `Cookies`. Для scheme настроен handler, который проверяет credentials.

</details>

---

### Senior: Почему `401` не равен `403`?

<details>
<summary>Ответ</summary>

`401` обычно означает, что пользователь не аутентифицирован или credentials невалидны. `403` означает, что пользователь известен, но доступ к ресурсу запрещён.

</details>

---

## Ответ для собеседования

Authentication в ASP.NET Core pipeline устанавливает, кто отправил request. Middleware вызывает authentication handler для выбранной scheme, например bearer token или cookie, и результатом становится `ClaimsPrincipal` в `HttpContext.User`. Если endpoint требует пользователя, а валидные credentials не предоставлены, обычно возвращается `401`. Важно не смешивать это с authorization: authentication отвечает за установление пользователя, а authorization проверяет доступ. JWT, refresh token, OAuth/OIDC и AuthService — отдельная тема Модуля III.

---

## Шпаргалка

- Authentication устанавливает пользователя.
- Credentials могут быть token или cookie.
- Scheme определяет способ проверки.
- Handler проверяет credentials.
- Результат попадает в `HttpContext.User`.
- `ClaimsPrincipal` представляет пользователя.
- `401` связан с отсутствием валидной authentication.
- Authorization проверяет доступ позже.
- Полная auth-система разбирается в Модуле III.

---

## Прогресс модуля

**Модуль II:** `ASP.NET Core Request Pipeline`  
**Прогресс после главы:** 63% (5 из 8 глав завершены).
