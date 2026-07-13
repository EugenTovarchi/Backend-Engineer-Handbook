# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 15. OpenIddict

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 82% (14 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** OpenIddict

**Текущий вопрос:**
Когда и как OpenIddict используется для OAuth 2.0 и OpenID Connect в .NET?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

OpenIddict нужен, когда .NET-приложение участвует в OAuth 2.0 / OpenID Connect scenarios как client, server или validation component. Глава должна отделить OpenIddict от ASP.NET Core Identity и показать, когда такой stack уместен.

## Границы главы

### Входит

- OpenIddict responsibilities;
- client/server/validation roles;
- relationship with ASP.NET Core;
- relationship with Identity;
- OAuth 2.0/OIDC endpoints and flows;
- when it is appropriate.

### Намеренно не входит

- statement that OpenIddict and ASP.NET Core Identity are the same;
- statement that OpenIddict is required for every AuthService;
- full production deployment.

## Эта глава понадобится позже

- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [Authorization Code Flow и PKCE](./12_Authorization_Code_PKCE.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 88% (15 из 17 глав завершены).
