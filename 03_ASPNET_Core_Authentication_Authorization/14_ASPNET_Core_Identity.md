# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 14. ASP.NET Core Identity

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 76% (13 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** ASP.NET Identity

**Текущий вопрос:**
Какие части управления пользователями и credentials уже предоставляет ASP.NET Core Identity?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

ASP.NET Core Identity предоставляет готовые компоненты для управления пользователями, password credentials, roles, claims и external logins. Глава нужна, чтобы понять его ответственность и не смешивать Identity с OAuth/OIDC server.

## Границы главы

### Входит

- users;
- password hasher;
- `UserManager`;
- `SignInManager`;
- stores;
- roles;
- claims;
- security stamp;
- external logins;
- local application scenario.

### Намеренно не входит

- claim that Identity is an OAuth/OIDC server;
- mandatory use in every project;
- UI scaffolding in depth.

## Эта глава понадобится позже

- [Учётная запись, credentials и хранение пользователей](./02_User_Accounts_Credentials_Storage.md)
- [Парольная аутентификация и безопасное хранение паролей](./03_Password_Authentication_Storage.md)
- [Cookie Authentication и аутентифицированная session](./05_Cookie_Authentication_Session.md)
- [Claims, Roles и Permissions](./09_Claims_Roles_Permissions.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [OpenIddict](./15_OpenIddict.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 82% (14 из 17 глав завершены).
