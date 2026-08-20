# Занятие: одна заметка × пирамида

Живой отчёт. Обновлять **в конце фазы**. PDF и PR — только по OK человека.

HTTP-глаголы **не дублировать** здесь — SSOT: [`note-http`](../agent-skills/rag/note-http.md).

## Цель

Одна заметка на пользователя (без списка). HTTP — RFC/MDN, не учебный POST+409.  
«100% пирамиды» = каждый сценарий на своём `@Layer` (`test-pyramid`).  
Не 100% строк JaCoCo. Не e2e на все глаголы. Slice (`smoke` / `screenshot` / `mock`) ≠ слой.

Продукт: логин/регистрация + health/items + синглтон `/api/note` и `note-panel`. Ярусы takeaway — после «следующий ярус».

## ADR

| ADR | Статус | Суть |
|-----|--------|------|
| [005](../adr/005-screenshot-not-layer.md) | принято | screenshot/mock/smoke — slice, не `@Layer` |
| [006](../adr/006-one-note-not-list.md) | **принято** | синглтон `/api/note`; RFC не POST+409; delete на prod — фабрика |

## Таблица: сценарий × ярус

Ячейка: `—` = не этот ярус; `план` = свой ярус, теста ещё нет; дальше — класс#метод.  
Слоты по `note-http` + `test-pyramid`.

| Сценарий | Свой ярус | unit | integration | component | api | e2e | manual | Стенды |
|----------|-----------|:----:|:-----------:|:---------:|:---:|:---:|:------:|--------|
| PUT create-or-replace: один ряд | unit | план | — | — | — | — | — | n/a (unit) |
| Persist PUT / GET / PATCH / DELETE | integration | — | план | — | — | — | — | pipeline |
| Форма title+text, без списка | component | — | — | план | — | — | — | n/a (jsdom) |
| HTTP PUT 201/200, PATCH, 401/400/404/415/422 | api | — | — | — | план | — | — | pipeline / stage / prod (delete — фабрика, не `user1`) |
| Пользователь сохраняет и видит заметку | e2e | — | — | — | — | план | — | pipeline / stage; prod — узкий smoke, не все глаголы |
| Delete / destructive UX | manual + api | — | — | — | план* | — | план | api DELETE: все стенды; фабрика + teardown |

\* api-delete — тот же ярус `api`. PATCH vs PUT — тоже `api`, не два e2e.

Покрытие takeaway: **0/6 ярусов**. Фича в коде есть. Backend unit/integration под JaCoCo — quality gate модуля, не ярусы пака (`tests-java-…`).

## Лог фаз

| Фаза | Что | Файлы | Прогон | Exit | Итог |
|------|-----|-------|--------|------|------|
| 0 | оркестратор + ADR + отчёт + PACK | skill `qa-make-full-pyramid`; ADR 006; этот файл; PACK | нет | n/a | артефакты есть |
| 1 | контракт | ADR 006; сначала CRUD-POST | нет | n/a | затем сверка RFC |
| 1b | канон RFC | RAG `note-http`; ADR 006 | нет | n/a | POST убран; PUT 201/200 |
| 1c | SSOT | `note-http` в monorepo RAG + диета; generic skills без таблицы глаголов | нет | n/a | план ссылается на RAG |
| 2 | backend | `V3__notes.sql`; `NoteController`/`NoteService`; JaCoCo-тесты модуля | `./gradlew test jacocoTestCoverageVerification` | 0 | PUT 201/200, PATCH merge-patch, cascade delete |
| 3 | frontend | `lib/note.ts`; `note-panel` на Home; stub GET `/api/note` в `HomePage.test` | `npm test` | 0 | Save = PUT; PATCH с UI нет |

## Вывод: зачем skills / rules / RAG / ADR

| Слой | Роль на этом занятии |
|------|----------------------|
| **Skill** | `qa-make-full-pyramid` = один ярус + STOP; api/e2e — `qa-write-test`; план дыр — `qa-pyramid-plan`. |
| **Rule** | Нет commit без OK; один `@Layer`; URL не в Java; сиды не сносить (`cfg-stands`). |
| **RAG** | `note-http` = палата мер HTTP; `cfg-stands` = стенды; плюс 2–3 чанка яруса. |
| **ADR** | Почему синглтон и RFC, не POST+409 (006); screenshot не слой (005). |

Без связки агент пишет e2e на все глаголы, путает 100% с JaCoCo или возвращает POST+409.

## Что осталось человеку

- Ярусы takeaway — «следующий ярус» (`qa-make-full-pyramid`), по одному чату.
- Stage / PDF / PR — только явным OK. Commit — тоже.
