# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 9. Claims, Roles и Permissions

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 47% (8 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Claims

**Текущий вопрос:**
Как представить сведения о субъекте и его правах так, чтобы система могла принимать решения о доступе?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Claims, roles и permissions нужны, чтобы описывать субъект и его возможности в форме, пригодной для authorization. Глава должна отделить сведения о субъекте от правил принятия решения, которые будут разобраны в следующей главе.

## Границы главы

### Входит

- claims model;
- roles;
- permissions;
- trust and issuer;
- stale claims;
- token-size consequences.

### Намеренно не входит

- requirements and handlers;
- full JWT format;
- database schema for every authorization model.

## Эта глава понадобится позже

- [Кто обращается к системе: Identity, Authentication и Authorization](./01_Identity_Authentication_Authorization.md)
- [JWT и проверка token](./07_JWT_Token_Validation.md)
- [Policy-based и Resource-based Authorization в ASP.NET Core](./10_Policy_Resource_Authorization.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [OpenIddict](./15_OpenIddict.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 53% (9 из 17 глав завершены).
