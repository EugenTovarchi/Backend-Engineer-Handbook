# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 12. Authorization Code Flow и PKCE

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 65% (11 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Code + PKCE

**Текущий вопрос:**
Как redirect-based client безопасно получает tokens через authorization server?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Authorization Code Flow + PKCE является ключевым redirect-based flow для получения tokens через authorization server. Глава нужна, чтобы отдельно разобрать code, redirect URI, PKCE и threat model, не смешивая это с OIDC identity layer.

## Границы главы

### Входит

- authorization request;
- redirect URI;
- authorization code;
- token endpoint;
- code verifier;
- code challenge;
- `S256`;
- `state`;
- threat model.

### Намеренно не входит

- complete ID Token semantics;
- provider-specific setup;
- ASP.NET Core Identity internals.

## Эта глава понадобится позже

- [Cookie Authentication и аутентифицированная session](./05_Cookie_Authentication_Session.md)
- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [OpenIddict](./15_OpenIddict.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 71% (12 из 17 глав завершены).
