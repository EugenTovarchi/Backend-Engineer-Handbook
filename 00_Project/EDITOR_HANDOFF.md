# Editor Handoff

Документ для быстрого входа в проект новым чатом ChatGPT или новой CLI-сессией.

## Проект

`Backend Engineer Handbook`

Репозиторий:

```text
https://github.com/EugenTovarchi/Backend-Engineer-Handbook
```

Подзаголовок:

> Понимание технологий через путешествие одного запроса.

## Цель книги

Создать инженерную книгу для .NET / ASP.NET Core backend-разработчика уровня Middle+.

Книга должна помогать:

- готовиться к собеседованиям;
- понимать реальные backend-системы;
- связывать технологии в один путь запроса;
- объяснять решения простым, но технически точным языком.

## Главный принцип

> Не запоминай технологии.
> Понимай, какие проблемы они решают.

Каждая глава должна отвечать не только на вопрос `что это`, но и на вопрос `какую инженерную проблему это решает`.

## Источники истины

Приоритет источников:

```text
STYLE_GUIDE
  ↓
BOOK_DECISIONS
  ↓
ROADMAP
  ↓
PROJECT_STATUS
  ↓
готовые главы
```

Если документы конфликтуют, сначала ориентироваться на `STYLE_GUIDE.md`, затем на `BOOK_DECISIONS.md`.

## Что уже завершено

- Репозиторий книги создан.
- `README.md` создан.
- `ROADMAP.md` создан.
- `STYLE_GUIDE.md` создан.
- Модуль I `Путешествие одного запроса` написан полностью.
- Модуль I прошёл первый редакторский проход:
  - унифицированы шапки глав;
  - введён единый маршрут;
  - введён прогресс до/после главы;
  - заменены Obsidian wiki-links на Markdown-ссылки;
  - удалены блоки `Когда не нужно уходить глубже`;
  - унифицирована терминология.
- Модуль II `ASP.NET Core Request Pipeline: от Kestrel до Endpoint` завершён и утверждён пользователем:
  - 8 из 8 глав созданы;
  - пользовательский review завершён;
  - финальный редакторский проход завершён;
  - содержательные правки без отдельного запроса не запланированы.
- Модуль III `Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect` начат:
  - создана папка `03_ASPNET_Core_Authentication_Authorization`;
  - созданы 17 из 17 файлов глав;
  - главы 1–4 написаны как первичные полные версии;
  - первый технический корректирующий проход глав 1–4 выполнен;
  - исправлены subject/account/provider/credential, password hashing sequence, NIST SP 800-63B-4 guidance и поток ASP.NET Core Authentication;
  - главы 5–8 написаны как первичные полные версии в понятном формате Модуля I;
  - главы 1–8 ожидают пользовательский и технический review и ещё не утверждены;
  - главы 9–17 содержат только архитектурный каркас.

Commit первого редакторского прохода:

```text
167f69d58af98e074966532fd3ee246e9327e051
```

## Что находится в Review

- Модульная структура книги.
- Блок `Связи внутри модуля`.
- Использование компактного горизонтального индикатора прогресса.
- Отказ от большой карты модуля в каждой главе.
- Финальное утверждение Модуля I пользователем.
- CORS как кандидат для будущего Модуля V.

## Текущий модуль

Завершённый модуль:

```text
Модуль II. ASP.NET Core Request Pipeline: от Kestrel до Endpoint
```

Статус:

```text
Модуль II утверждён пользователем.
Пользовательский review завершён.
Финальный редакторский проход завершён.
Содержательные правки Модуля II без отдельного запроса не запланированы.
Последний содержательный commit Модуля II: fc34ed6c44d77e95e83fc13280fd128257b888a2.
```

Цель модуля — объяснить, что происходит после того, как HTTP-запрос достиг .NET-приложения:

- как Kestrel передаёт запрос в ASP.NET Core;
- зачем нужен `HttpContext`;
- как middleware образуют pipeline;
- как routing выбирает endpoint;
- как authentication устанавливает пользователя;
- как authorization проверяет доступ;
- когда выполняется controller action или Minimal API handler;
- как response возвращается через pipeline.

Маршрут Модуля II:

```text
Kestrel → HttpContext → Middleware → Routing → Authentication → Authorization → Endpoint → Full Pipeline
```

Главы Модуля II:

1. Граница Kestrel и ASP.NET Core
2. HttpContext
3. Middleware Pipeline
4. Routing и выбор Endpoint
5. Authentication внутри Pipeline
6. Authorization внутри Pipeline
7. Выполнение выбранного Endpoint
8. Полный ASP.NET Core Request Pipeline

Текущая рабочая тема:

```text
Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect.
```

Архитектура и маршрут Модуля III утверждены пользователем. Текущий рабочий блок — главы 1–8.

Полностью написанные первичные версии:

1. `01_Identity_Authentication_Authorization.md`
2. `02_User_Accounts_Credentials_Storage.md`
3. `03_Password_Authentication_Storage.md`
4. `04_ASPNET_Core_Authentication_Model.md`
5. `05_Cookie_Authentication_Session.md`
6. `06_Access_Token_Bearer_Authentication.md`
7. `07_JWT_Token_Validation.md`
8. `08_Refresh_Token_Lifecycle.md`

Главы 5–8 написаны в формате подачи Модуля I: сначала проблема и базовый flow простыми словами, затем ASP.NET Core/API и только после этого security и production-ограничения.

Главы 1–8 готовы к review, но ещё не утверждены пользователем. Главы 9–17 пока являются только архитектурным каркасом. Главы 9–17 не писать без отдельного задания. Модуль II не менять без отдельного запроса.

Маршрут Модуля III:

1. Кто обращается к системе: Identity, Authentication и Authorization
2. Учётная запись, credentials и хранение пользователей
3. Парольная аутентификация и безопасное хранение паролей
4. Модель Authentication в ASP.NET Core
5. Cookie Authentication и аутентифицированная session
6. Access Token и Bearer Authentication
7. JWT и проверка token
8. Refresh Token и жизненный цикл token
9. Claims, Roles и Permissions
10. Policy-based и Resource-based Authorization в ASP.NET Core
11. OAuth 2.0: делегирование доступа, роли и scopes
12. Authorization Code Flow и PKCE
13. OpenID Connect и внешние Identity Providers
14. ASP.NET Core Identity
15. OpenIddict
16. Архитектура AuthService и границы distributed system
17. Полный путь аутентификации и авторизации

Границы scope:

- Authentication и Authorization в Модуле II рассматриваются только как этапы request pipeline.
- Полная authentication-система не удалена из книги и будет разобрана в Модуле III.
- JWT, access token, refresh token, OAuth 2.0, OpenID Connect, ASP.NET Core Identity, хранение пользователей и AuthService относятся к Модулю III.
- Nginx, Reverse Proxy, Load Balancer, API Gateway, YARP, Forwarded Headers, TLS termination и Docker Networking относятся к Модулю IV.
- Controllers, Minimal APIs, Filters, Model Binding, Validation, ProblemDetails, Dependency Injection, Configuration, Hosted Services, Health Checks, API Versioning, OpenAPI и Rate Limiting восстановлены как scope будущего Модуля V.

Границы scope Модуля III:

- Authentication не сводится к JWT.
- Cookie Authentication и token-based authentication рассматриваются как разные модели.
- Password Hashing, Cookie Authentication, Access Token, JWT validation и Refresh Token lifecycle разделены.
- Claims, Roles и Permissions отделены от Policy-based и Resource-based Authorization.
- OAuth 2.0 и OpenID Connect не смешиваются.
- ASP.NET Core Identity, OpenIddict и AuthService разделяются по ответственности.
- Отдельный AuthService не считается обязательным для каждого проекта.
- Security threats и типичные ошибки раскрываются рядом с механизмами и сводятся в итоговой главе, без отдельной изолированной главы.
- CORS не переносится в Модуль III автоматически.
- CSRF раскрывается в темах Cookie Authentication и redirect-based flows.

Последовательность ближайших модулей:

1. Модуль III — Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect.
2. Модуль IV — Production Entry Layer.
3. Модуль V — ASP.NET Core Web API и инфраструктура приложения.

## Как продолжать работу

1. Перед началом нового модуля прочитать:
   - `00_Project/STYLE_GUIDE.md`;
   - `00_Project/BOOK_DECISIONS.md`;
   - `00_Project/ROADMAP.md`;
   - `00_Project/PROJECT_STATUS.md`;
   - `00_Project/EDITOR_HANDOFF.md`.
2. Уточнить у пользователя, какой модуль или глава начинается.
3. Не менять уже завершённые главы без отдельного запроса.
4. Для каждой новой главы соблюдать структуру из `STYLE_GUIDE.md`.
5. Термины объяснять при первом появлении в главе.
6. Не повторять полностью термины, уже разобранные раньше; использовать короткое напоминание и ссылку.
7. После завершения модуля обновить `PROJECT_STATUS.md` и `CHANGELOG.md`.
8. Не писать главы 9–17 Модуля III до отдельного задания.
9. Модуль II не менять без отдельного запроса.

## Что запрещено менять

Без отдельного запроса нельзя:

- переписывать готовые главы;
- менять основную идею книги;
- удалять полезные технические примеры;
- создавать второй репозиторий;
- переписывать историю Git;
- делать force push;
- превращать книгу в рекламный текст;
- приписывать автору неподтверждённый опыт;
- расширять глубину главы за пределы потребностей Middle .NET Backend-разработчика.

## Как работать с Codex CLI

Codex CLI используется как исполнитель:

- проверяет `git status`;
- выполняет `git pull`, если рабочая директория чистая;
- редактирует Markdown-файлы;
- показывает `git diff --stat`;
- выполняет проверки;
- делает один осмысленный commit;
- выполняет push.

Рекомендуемый цикл:

```text
read project docs
  ↓
check git status
  ↓
pull
  ↓
edit files
  ↓
check diff
  ↓
run markdown checks
  ↓
commit
  ↓
push
```

Если в рабочей директории есть чужие незакоммиченные изменения, Codex CLI должен остановиться и сообщить о них пользователю.
