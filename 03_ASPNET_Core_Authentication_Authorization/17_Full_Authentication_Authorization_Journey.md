# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 17. Полный путь аутентификации и авторизации

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 94% (16 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Full Journey

**Текущий вопрос:**
Как локальный login, cookies, tokens, authorization и внешние providers складываются в целостную систему?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Итоговая глава нужна, чтобы собрать локальный login, cookies, access tokens, refresh lifecycle, external providers и authorization decisions в одну инженерную картину. Она должна стать проверкой, что механизмы не смешаны и не противоречат друг другу.

## Границы главы

### Входит

Будущая итоговая сборка сценариев:

1. local password + cookie;
2. local password + Access Token;
3. refresh and rotation;
4. external OIDC login;
5. authorization decision;
6. logout/revocation/expiration;
7. diagnostics by layers.

### Намеренно не входит

- новые механизмы;
- новая теория;
- повтор полного текста всех глав.

## Эта глава понадобится позже

- [Кто обращается к системе: Identity, Authentication и Authorization](./01_Identity_Authentication_Authorization.md)
- [Cookie Authentication и аутентифицированная session](./05_Cookie_Authentication_Session.md)
- [Access Token и Bearer Authentication](./06_Access_Token_Bearer_Authentication.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [Policy-based и Resource-based Authorization в ASP.NET Core](./10_Policy_Resource_Authorization.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный ASP.NET Core Request Pipeline](../02_ASPNET_Core_Request_Pipeline/08_Full_ASPNET_Core_Request_Pipeline.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 100% (17 из 17 глав завершены).
