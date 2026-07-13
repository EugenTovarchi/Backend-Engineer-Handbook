# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 6. Access Token и Bearer Authentication

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 29% (5 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Access Token

**Текущий вопрос:**
Как API принимает credential без browser cookie и почему Bearer Token требует особой защиты?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Access Token нужен API, чтобы принимать credential без browser session cookie. Глава покажет, почему bearer-предъявление удобно для API и почему украденный bearer token опасен: кто предъявил token, тот получает доступ в пределах его срока и scope.

## Границы главы

### Входит

- Access Token purpose;
- Bearer presentation;
- opaque vs self-contained overview;
- resource server;
- token transport and theft risk.

### Намеренно не входит

- JWT internal format;
- refresh flow;
- OAuth authorization flow.

## Эта глава понадобится позже

- [Модель Authentication в ASP.NET Core](./04_ASPNET_Core_Authentication_Model.md)
- [JWT и проверка token](./07_JWT_Token_Validation.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [OAuth 2.0: делегирование доступа, роли и scopes](./11_OAuth2_Delegated_Access.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 35% (6 из 17 глав завершены).
