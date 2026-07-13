# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 11. OAuth 2.0: делегирование доступа, роли и scopes

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 59% (10 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** OAuth 2.0

**Текущий вопрос:**
Как предоставить client ограниченный доступ к resource без передачи credentials пользователя?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

OAuth 2.0 нужен для delegated access: client получает ограниченный доступ к resource без передачи ему credentials пользователя. Глава должна отделить OAuth 2.0 от OpenID Connect и от бытовой формулировки "вход через Google".

## Границы главы

### Входит

- delegated access;
- resource owner;
- client;
- authorization server;
- resource server;
- scopes;
- grants overview;
- Client Credentials overview.

### Намеренно не входит

- detailed Authorization Code + PKCE;
- ID Token;
- «вход через Google» как определение OAuth.

## Эта глава понадобится позже

- [Access Token и Bearer Authentication](./06_Access_Token_Bearer_Authentication.md)
- [JWT и проверка token](./07_JWT_Token_Validation.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [Authorization Code Flow и PKCE](./12_Authorization_Code_PKCE.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [OpenIddict](./15_OpenIddict.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 65% (11 из 17 глав завершены).
