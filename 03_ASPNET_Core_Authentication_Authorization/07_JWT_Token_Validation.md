# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 7. JWT и проверка token

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 35% (6 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** JWT

**Текущий вопрос:**
Как resource server проверяет self-contained token и почему одной проверки подписи недостаточно?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

JWT часто воспринимают как всю authentication-систему, но это только token format. Глава нужна, чтобы отдельно разобрать структуру JWT и validation rules, не смешивая их с refresh lifecycle, OAuth flow и выпуском token.

## Границы главы

### Входит

- JWT structure;
- signing vs encryption;
- issuer;
- audience;
- lifetime;
- algorithms;
- key rotation;
- JWT Bearer validation.

### Намеренно не входит

- refresh lifecycle;
- OAuth flow;
- custom cryptography.

## Эта глава понадобится позже

- [Access Token и Bearer Authentication](./06_Access_Token_Bearer_Authentication.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 41% (7 из 17 глав завершены).
