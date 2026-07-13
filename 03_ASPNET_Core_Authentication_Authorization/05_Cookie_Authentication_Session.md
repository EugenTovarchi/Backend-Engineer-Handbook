# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 5. Cookie Authentication и аутентифицированная session

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 24% (4 из 17 глав завершены)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Cookie

**Текущий вопрос:**
Как браузер сохраняет состояние входа между HTTP-запросами и что именно проверяет Cookie Authentication?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

> **Статус главы: создан архитектурный каркас.** Полный текст будет написан отдельным заданием.

## Зачем нужна эта глава

Cookie Authentication объяснит browser-oriented модель входа, где состояние аутентификации переносится между запросами через cookie. Глава нужна, чтобы отделить cookie session от bearer token модели и показать, почему CSRF относится прежде всего к cookie и redirect-based сценариям.

## Границы главы

### Входит

- authentication cookie;
- authentication ticket;
- session concept;
- server-side ticket store;
- expiration;
- sliding expiration;
- sign-in/sign-out;
- Data Protection;
- cookie security attributes;
- CSRF.

### Намеренно не входит

- JWT;
- OAuth redirect flow;
- ASP.NET Core Identity как framework;
- CORS как основная тема.

## Эта глава понадобится позже

- [Модель Authentication в ASP.NET Core](./04_ASPNET_Core_Authentication_Model.md)
- [Refresh Token и жизненный цикл token](./08_Refresh_Token_Lifecycle.md)
- [Authorization Code Flow и PKCE](./12_Authorization_Code_PKCE.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [Полный путь аутентификации и авторизации](./17_Full_Authentication_Authorization_Journey.md)

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 29% (5 из 17 глав завершены).
