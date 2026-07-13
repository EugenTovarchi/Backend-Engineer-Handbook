# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 16. Архитектура AuthService и границы distributed system

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 88% (15 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** AuthService

**Текущий вопрос:**
Когда auth-логику следует оставить внутри приложения, а когда выделять отдельную архитектурную границу?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

AuthService — архитектурная граница, а не обязательный компонент любого проекта. Глава нужна, чтобы разобрать tradeoffs между monolith, modular monolith и отдельным service без превращения темы в общий курс microservices.

## Границы главы

### Входит

- monolith;
- modular monolith;
- separate service;
- ownership of users and credentials;
- token issuance;
- signing keys;
- resource APIs;
- trust boundaries;
- availability;
- revocation propagation;
- distributed-system tradeoffs.

### Намеренно не входит

- general microservices course;
- API Gateway internals;
- claim that separate AuthService is mandatory.

## Эта глава понадобится позже

- [Учётная запись, credentials и хранение пользователей](./02_User_Accounts_Credentials_Storage.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [Claims, Roles и Permissions](./09_Claims_Roles_Permissions.md)
- [Policy-based и Resource-based Authorization в ASP.NET Core](./10_Policy_Resource_Authorization.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [OpenIddict](./15_OpenIddict.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 94% (16 из 17 глав завершены).
