# Project Status

Дата старта: 2026-07-09

## Текущее состояние

Проект создан как отдельный GitHub-репозиторий для будущей книги `Backend Engineer Handbook`.

Подзаголовок книги:

> Понимание технологий через путешествие одного запроса.

Исходная база знаний загружена из архива `Собеседования.zip`.

## Инфраструктурные документы проекта

- `STYLE_GUIDE.md` — главный источник правил оформления и качества глав.
- `BOOK_DECISIONS.md` — журнал архитектурных и редакционных решений книги.
- `EDITOR_HANDOFF.md` — краткий документ для продолжения работы в новом чате или новой CLI-сессии.
- `PROJECT_STATUS.md` — текущее состояние проекта.
- `ROADMAP.md` — рабочая структура будущей книги.
- `CHANGELOG.md` — редакционный журнал изменений книги.

## Что найдено в архиве

- Всего Markdown-файлов: 107
- Основные папки:
  - `STACK`
  - `МОЁ РЕЗЮМЕ ДЕФ ПРЕЗЕНТАЦИЯ`
  - `Backend Engineer Handbook`
- Папка `Backend Engineer Handbook` внутри архива пока пустая.
- Есть 2 пустых файла:
  - `STACK/EFCore Lazy ,Eager  Explicit loading(не готов).md`
  - `STACK/Events События (не готов).md`

## Самые крупные и ценные источники

- `STACK/Асинхронность и ThreadPool.md`
- `STACK/RabbitMQ.md`
- `STACK/GarbageCollector.md`
- `STACK/Индексы, данные в таблица, денормализация и JSON.md`
- `STACK/EFCore.md`
- `STACK/Value Types & Reference types.md`
- `STACK/Многопоточность и параллелизм.md`
- `STACK/AUTH.md`
- `STACK/DDD.md`
- `STACK/DI.md`
- `nginx-guide.md`
- `STACK/NGINX.md`
- `МОЁ РЕЗЮМЕ ДЕФ ПРЕЗЕНТАЦИЯ/Дефы/24_eye_interview_def_unified.md`

## Текущая рабочая тема

Текущий модуль: `Модуль II. ASP.NET Core Request Pipeline`.

Состояние:

- Модуль I написан полностью;
- 9 из 9 глав созданы в репозитории;
- первый редакторский проход Модуля I завершён;
- Модуль I ожидает финального review пользователем;
- структура Модуля II утверждена;
- восемь глав Модуля II созданы;
- первичный черновик Модуля II написан;
- Модуль II ещё не прошёл пользовательский review;
- Модуль II ещё не прошёл финальный редакторский проход;
- Модуль III будет посвящён authentication и authorization как полноценной инженерной теме.

Следующий практический этап: редакторская проверка Модуля II в рабочем чате.

## Review

- [ ] Формат `Модуль -> Глава` проверяется на первом модуле.
- [ ] Блок `Связи внутри модуля` пока не внедряется; вернуться к нему после завершения первого модуля.
- [ ] Большая карта модуля пока не используется в каждой главе.
- [ ] Вместо большой карты используется компактный горизонтальный индикатор прогресса модуля.
- [ ] После чтения модуля пользователем решить, оставляем ли модульную структуру.

## Прогресс первого модуля

**Модуль I:** `Путешествие одного запроса`  
**Прогресс модуля:** 9 из 9 глав — 100%.

Главы модуля:

1. `01_Request_Journey/01_URL.md`
2. `01_Request_Journey/02_DNS.md`
3. `01_Request_Journey/03_IP_Address.md`
4. `01_Request_Journey/04_Port.md`
5. `01_Request_Journey/05_TCP.md`
6. `01_Request_Journey/06_TLS.md`
7. `01_Request_Journey/07_HTTP.md`
8. `01_Request_Journey/08_HTTPS.md`
9. `01_Request_Journey/09_Full_Request_Journey.md`

## План Модуля II

**Модуль II:** `ASP.NET Core Request Pipeline`
**Статус:** первичный черновик написан, пользовательский review и финальный редакторский проход ещё не выполнены.

Главы модуля:

1. `02_ASPNET_Core_Request_Pipeline/01_Kestrel_ASPNET_Core_Boundary.md`
2. `02_ASPNET_Core_Request_Pipeline/02_HttpContext.md`
3. `02_ASPNET_Core_Request_Pipeline/03_Middleware_Pipeline.md`
4. `02_ASPNET_Core_Request_Pipeline/04_Routing_Endpoint_Selection.md`
5. `02_ASPNET_Core_Request_Pipeline/05_Authentication_In_Pipeline.md`
6. `02_ASPNET_Core_Request_Pipeline/06_Authorization_In_Pipeline.md`
7. `02_ASPNET_Core_Request_Pipeline/07_Endpoint_Execution.md`
8. `02_ASPNET_Core_Request_Pipeline/08_Full_ASPNET_Core_Request_Pipeline.md`

## Ближайшая последовательность модулей

1. Модуль II — ASP.NET Core Request Pipeline.
2. Модуль III — Аутентификация и авторизация.
3. Модуль IV — Production Entry Layer.

## Ближайший план

1. Передать Модуль II на редакторскую проверку в рабочем чате.
2. Внести правки по review Модуля II.
3. Провести финальный редакторский проход Модуля II.
4. Не считать Модуль II утверждённым до явного решения пользователя.
5. После завершения каждого модуля обновлять `PROJECT_STATUS.md` и `CHANGELOG.md`.

## Статусы

- [x] Репозиторий создан
- [x] README создан
- [x] Архив прочитан
- [x] Первичный аудит выполнен
- [x] Roadmap создан
- [x] Style Guide создан
- [x] Формат первой части переведен в Review как модульный эксперимент
- [x] Модуль I создан
- [x] Черновик Модуля I написан полностью
- [x] Модуль I прошёл первый редакторский проход
- [x] Book Decisions создан
- [x] Editor Handoff создан
- [x] Changelog создан
- [ ] Модуль I ожидает финального review пользователем
- [ ] Модуль I утверждён
- [x] Структура Модуля II утверждена
- [x] Модуль II создан
- [x] Первичный черновик Модуля II написан
- [ ] Модуль II прошёл пользовательский review
- [ ] Модуль II прошёл финальный редакторский проход
- [ ] Формат модулей принят или отклонён
