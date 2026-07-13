# Модуль III. Аутентификация и авторизация в ASP.NET Core: Cookies, JWT, OAuth 2.0 и OpenID Connect

# Глава 2. Учётная запись, credentials и хранение пользователей

──────────────────────────────────────────────

**МОДУЛЬ III • Аутентификация и авторизация**

**Прогресс до главы:** 6% (1 из 17 глав завершена)

**Маршрут:** Identity → Account → Password → Auth Schemes → Cookie → Access Token → JWT → Refresh Token → Claims → Policies → OAuth 2.0 → Code + PKCE → OIDC → ASP.NET Identity → OpenIddict → AuthService → Full Journey

**Текущая глава:** Account

**Текущий вопрос:**
Какие данные auth-система должна хранить, чтобы узнавать субъекта и управлять его способами входа?

──────────────────────────────────────────────

> **Не запоминай технологии. Понимай, какие проблемы они решают.**

---

## Исходная ситуация

В предыдущей главе мы отделили subject, credentials, authentication и authorization.

Теперь появляется практический вопрос:

```text
что именно хранить в базе, чтобы пользователь мог войти, сменить email, подключить внешний provider и не потерять устойчивую identity внутри системы?
```

Если хранить всё в одной записи вроде `User { Email, Password, Role }`, система быстро становится хрупкой: email меняется, пароль может быть заменён, внешний login не похож на локальный пароль, а permissions не должны жить в случайном profile field.

---

## Зачем нужна эта глава

Эта глава нужна, чтобы не строить authentication поверх случайной таблицы пользователей.

Auth-система должна хранить:

- стабильный внутренний идентификатор;
- изменяемые login identifiers;
- credentials;
- статусы account;
- признаки подтверждения email/phone;
- связи с внешними providers;
- технические markers для отзыва sessions или credentials.

Это не про полный ASP.NET Core Identity schema. Это про базовую модель данных, без которой сложно понять следующие главы.

---

## Эта глава понадобится позже

- [Кто обращается к системе: Identity, Authentication и Authorization](./01_Identity_Authentication_Authorization.md)
- [Парольная аутентификация и безопасное хранение паролей](./03_Password_Authentication_Storage.md)
- [OpenID Connect и внешние Identity Providers](./13_OpenID_Connect_External_Identity_Providers.md)
- [ASP.NET Core Identity](./14_ASPNET_Core_Identity.md)
- [Архитектура AuthService и границы distributed system](./16_AuthService_Distributed_Boundaries.md)

---

## Короткое определение

**User account (учётная запись пользователя — сохранённая запись системы, через которую backend связывает способы входа, состояние и внутреннюю identity)** не должна зависеть от одного изменяемого email или одного пароля.

**Login identifier (идентификатор входа — значение, по которому пользователь может начать вход)** может быть username, email или phone.

**Credential record (запись credential — сохранённые данные, по которым можно проверить способ входа или связать внешний login)** должна быть логически отделена от profile data.

---

## Простая аналогия

Учётная запись похожа на личное дело сотрудника.

Внутренний номер сотрудника стабилен. Email, телефон, пропуск, пароль от портала и внешний badge могут меняться. Если сделать email главным идентификатором всего сотрудника, любая смена email превращается в миграцию identity.

---

## Техническое объяснение

Auth-системе нужен стабильный `UserId`. Он не обязан быть видим пользователю и не должен меняться при смене email, username или phone.

Изменяемые идентификаторы входа лучше хранить отдельно или явно нормализовать:

- username;
- email;
- phone.

Email не стоит автоматически считать primary key:

- пользователь может сменить email;
- email может требовать подтверждения;
- правила нормализации зависят от системы;
- в некоторых системах один человек может иметь несколько verified identifiers;
- внешний provider может вернуть другой stable subject, не равный локальному email.

Уникальность login identifier должна защищаться не только кодом приложения, но и ограничением базы: уникальным индексом. Предварительный `SELECT` перед вставкой полезен для friendly error, но не защищает от race condition.

Account status обычно включает:

| Статус | Смысл |
|---|---|
| Active | учётная запись может использоваться |
| Disabled | вход отключён администратором или политикой |
| Locked | вход временно ограничен после риска или ошибок |
| Deleted | запись удалена или помечена как удалённая концептуально |

Email/phone confirmation — отдельное состояние. Пользователь может существовать, но email ещё не подтверждён. Это не то же самое, что account disabled.

Один account может иметь несколько credentials:

- password credential;
- external login mapping;
- позже возможны passkeys, API keys или другие способы входа.

Profile data тоже стоит отделять от authentication data. Имя, аватар, язык интерфейса и должность — это не credentials и не permissions.

---

## Схема

```mermaid
flowchart TD
    A[UserAccount] --> L[Login identifiers]
    A --> P[PasswordCredential]
    A --> E[ExternalLogin]
    A --> S[Account status]
    A --> M[Security marker]
    A --> R[Profile data]
```

---

## Практический сценарий

Пользователь зарегистрировался по email, потом:

1. подтвердил email;
2. сменил email;
3. подключил вход через внешний provider;
4. сбросил пароль;
5. получил временную блокировку после подозрительных попыток входа.

Если `UserId` стабилен, все эти операции не ломают ownership данных в домене: заказы, файлы и настройки остаются привязаны к тому же внутреннему субъекту. Меняются только способы входа и состояние account.

---

## Мини-пример модели

Это учебная модель, а не универсальная production-схема:

```csharp
public sealed class UserAccount
{
    public Guid Id { get; init; }
    public string NormalizedEmail { get; set; } = "";
    public bool EmailConfirmed { get; set; }
    public AccountStatus Status { get; set; }
    public string SecurityStamp { get; set; } = "";
}

public sealed class PasswordCredential
{
    public Guid UserId { get; init; }
    public string PasswordHash { get; set; } = "";
    public DateTimeOffset UpdatedAt { get; set; }
}

public sealed class ExternalLogin
{
    public Guid UserId { get; init; }
    public string Provider { get; init; } = "";
    public string ProviderSubject { get; init; } = "";
}
```

`SecurityStamp` здесь показан как общий security/revocation marker: при смене пароля или критичных credential-событиях система может использовать похожую идею для инвалидирования старых sessions или проверки актуальности state. Детали ASP.NET Core Identity будут позже.

---

## Типичные ошибки

Ошибка: хранить пароль в поле `Password` или `EncryptedPassword`.
Почему неверно: системе не нужен исходный пароль для проверки входа.
Как правильно: хранить password verifier, созданный password hashing scheme; подробнее это разбирается в следующей главе.

Ошибка: делать email неизменяемым primary key.
Почему неверно: email может измениться, быть неподтверждённым или прийти из внешнего provider.
Как правильно: использовать стабильный внутренний `UserId`.

Ошибка: хранить только `IsAuthenticated`.
Почему неверно: authentication — runtime-результат запроса, а не вся модель account.
Как правильно: хранить состояние account и credentials отдельно.

Ошибка: смешивать profile, credentials и permissions в одну неструктурированную запись.
Почему неверно: эти данные имеют разный lifecycle и разные требования безопасности.
Как правильно: разделять authentication data, profile data и authorization model.

Ошибка: обеспечивать уникальность login identifier только через `SELECT`.
Почему неверно: два параллельных запроса могут пройти проверку одновременно.
Как правильно: использовать уникальный индекс в базе и обрабатывать конфликт.

---

## Вопросы собеседования

### Junior: Почему системе нужен внутренний `UserId`?

<details>
<summary>Ответ</summary>

Потому что email, username и phone могут изменяться. Внутренний `UserId` остаётся стабильной связью между account и доменными данными.

</details>

---

### Middle: Почему проверка уникальности email в коде не заменяет unique index?

<details>
<summary>Ответ</summary>

Из-за race condition. Два запроса могут одновременно увидеть, что email свободен, и оба попытаться создать account. Окончательную гарантию уникальности должна давать база данных.

</details>

---

### Middle: Чем account отличается от credential?

<details>
<summary>Ответ</summary>

Account — это устойчивая запись субъекта в системе. Credential — конкретный способ подтвердить контроль: password hash, внешний login mapping или другой механизм входа. У одного account может быть несколько credentials.

</details>

---

### Senior: Зачем отделять authentication data от profile data?

<details>
<summary>Ответ</summary>

У них разные требования и жизненный цикл. Profile data можно менять без security-события, а credential changes могут требовать re-authentication, session revocation, audit и обновления security marker.

</details>

---

### Architect / System Design: Как внешний provider связан с локальным account?

<details>
<summary>Ответ</summary>

Внешний provider обычно даёт provider name и стабильный subject у себя. Локальная система связывает эту пару с внутренним `UserId`. Нельзя считать внешний account тем же самым, что локальный `UserId`: это mapping между двумя identity spaces.

</details>

---

## Ответ для собеседования

В auth-системе я бы разделял учётную запись, login identifiers, credentials и profile data. У пользователя должен быть стабильный внутренний `UserId`, потому что email, phone или username могут изменяться. Credentials лучше хранить отдельно: password credential, external login mapping и другие способы входа имеют разный lifecycle. Email confirmation, account status, lockout и security marker — это отдельные состояния, а не одно поле `IsAuthenticated`. Уникальность login identifiers должна подтверждаться уникальным индексом в базе, потому что проверка только на уровне приложения не защищает от гонок.

---

## Шпаргалка

- Account — стабильная запись системы.
- `UserId` должен быть внутренним и устойчивым.
- Email не стоит автоматически делать primary key.
- Login identifiers нужно нормализовать.
- Уникальность защищает база, не только код.
- Email/phone confirmation — отдельное состояние.
- Account может иметь несколько credentials.
- Password credential и external login mapping — разные вещи.
- Profile data не равен authentication data.
- Permissions не нужно прятать в profile blob.
- Security marker помогает отзывать старое состояние.

---

## Прогресс модуля

**Модуль III:** `Аутентификация и авторизация в ASP.NET Core`
**Прогресс после главы:** 12% (2 из 17 глав завершены).
