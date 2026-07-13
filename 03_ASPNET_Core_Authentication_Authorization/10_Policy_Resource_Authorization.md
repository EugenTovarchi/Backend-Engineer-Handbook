# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 10. Policy-based и Resource-based Authorization в ASP.NET Core

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 53% (9 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Policies

**Текущий вопрос:**
Как превратить claims и сведения о ресурсе в явное и тестируемое решение о доступе?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Authorization decision должен быть явным, тестируемым и отделённым от случайных checks в handlers. Глава объяснит policies, requirements, handlers и resource-based checks как модель принятия решения о доступе.

## Границы главы

### Входит

- policies;
- requirements;
- handlers;
- `IAuthorizationService`;
- role/claim/permission/resource-based checks;
- challenge and forbid.

### Намеренно не входит

- general business validation;
- filters;
- complete Web API execution.

## Эта глава понадобится позже

- [Кто обращается к системе: Identity, Authentication и Authorization](./01_Identity_Authentication_Authorization.md)
- [Модель Authentication в ASP.NET Core](./04_ASPNET_Core_Authentication_Model.md)
- [Claims, Roles и Permissions](./09_Claims_Roles_Permissions.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 59% (10 из 17 глав завершены).
