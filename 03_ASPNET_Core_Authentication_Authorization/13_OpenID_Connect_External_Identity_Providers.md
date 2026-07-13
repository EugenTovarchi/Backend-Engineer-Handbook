# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 13. OpenID Connect и внешние Identity Providers

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 71% (12 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** OIDC

**Текущий вопрос:**
Как приложение устанавливает личность пользователя через внешний Identity Provider поверх OAuth 2.0?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

OpenID Connect добавляет identity layer поверх OAuth 2.0. Глава нужна, чтобы отделить delegated access от установления личности пользователя через внешний Identity Provider.

## Границы главы

### Входит

- identity layer over OAuth 2.0;
- ID Token;
- Access Token distinction;
- `openid` scope;
- issuer;
- audience;
- subject;
- nonce;
- discovery;
- external providers.

### Намеренно не входит

- using ID Token as API Access Token;
- SAML;
- building a provider from scratch.

## Эта глава понадобится позже

- [Claims, Roles и Permissions](./09_Claims_Roles_Permissions.md)
- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [Authorization Code Flow и PKCE](./12_Authorization_Code_PKCE.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [OpenIddict](./15_OpenIddict.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 76% (13 из 17 глав завершены).
