# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 8. Refresh Token и жизненный цикл token

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 41% (7 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Refresh Token

**Текущий вопрос:**
Как продлевать доступ без повторного ввода credentials и ограничивать последствия компрометации?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Refresh Token нужен, чтобы продлевать доступ без постоянного повторного ввода credentials. Глава должна отделить короткоживущий access token от долгоживущего механизма обновления и показать lifecycle, revocation и compromise response.

## Границы главы

### Входит

- issuance;
- storage;
- expiration;
- rotation;
- token family;
- reuse detection;
- revocation;
- logout;
- compromise response.

### Намеренно не входит

- full OAuth redirect flow;
- cookie internals;
- ID Token semantics.

## Эта глава понадобится позже

- [Cookie Authentication и аутентифицированная session](./05_Cookie_Authentication_Session.md)
- [Access Token и Bearer Authentication](./06_Access_Token_Bearer_Authentication.md)
- [JWT и проверка token](./07_JWT_Token_Validation.md)
- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 47% (8 из 17 глав завершены).
