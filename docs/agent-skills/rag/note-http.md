---
id: note-http
domain: testing
adr: 006
tags: [http, rest, note, rfc]
related: [test-api-layer, cfg-stands, test-pyramid]
---
# HTTP заметки (RFC / MDN)

**id:** `note-http`

Канон **этого** репо: этот файл. Таблицу глаголов не копировать в skills.

Синглтон `/api/note`, `authenticated`. Нет коллекции, `{id}`, **нет POST**.

Канон: [RFC 9110 PUT](https://www.rfc-editor.org/rfc/rfc9110.html#name-put) · [MDN PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PUT) · [RFC 5789 PATCH](https://datatracker.ietf.org/doc/html/rfc5789) · [RFC 7396](https://www.rfc-editor.org/rfc/rfc7396.html).  
Почему: учебный ADR `docs/adr/006-one-note-not-list.md`.

| Метод | Тело | Успех | Ошибки |
|-------|------|-------|--------|
| `PUT` | `application/json`: оба ключа `title`, `text` | **201** создал (`Content-Location: /api/note`) / **200** заменил | 401, 400 |
| `GET` | — | 200 `{id,title,text}` | 401, **404** |
| `PATCH` | **`application/merge-patch+json`**, любое подмножество | **200** | 401, **404** нет ресурса, **415** не тот тип, 400 malform, **422** результат невалиден |
| `DELETE` | без тела | **204** | 401, **404** |

`title` 0…120; в PATCH JSON `null` снимает поле — в модели это `""`. `text` 1…2000; `null` в PATCH → **422**.  
PATCH `{}` — no-op → **200**. PUT без `id`. Повторный PUT идемпотентен, не 409.  
415 на PATCH: `Accept-Patch: application/merge-patch+json`.

Чужая заметка: другой JWT → свой синглтон (пусто = 404).

Delete на prod: фабрика + teardown, не сид `user1` (`cfg-stands` + ADR 006).

UI: `note-panel` (`note-title-input`, `note-input`, `note-save-button` = **PUT**, `note-delete-button`). Без списка. PATCH — только api.

## Don't

- `POST /api/note` и 409 «already exists»
- PUT, который не создаёт (404 вместо 201)
- PATCH с `application/json` без **415**
- Закрывать PUT/PATCH только e2e
- Delete сида `user1` на prod
