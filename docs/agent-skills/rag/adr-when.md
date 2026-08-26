---
id: adr-when
domain: testing
adr: 005
tags: [adr, rag, skill, rule]
related: [test-pyramid, test-api-layer, test-negative]
---
# Когда писать ADR

**id:** `adr-when`

| Вопрос | Куда |
|--------|------|
| Что нельзя / всегда так? | **Rule** (короткий лимит) |
| Как сделать задачу сегодня? | **Skill** (шаги + DoD) |
| Откуда факт / якорь / команда? | **RAG** (2–4 чанка) |
| Почему выбрали A, а не B — надолго? | **ADR** |

ADR пишут, когда решение **дорого откатывать**: ярус vs slice (005), Rest Assured vs e2e на 401 (009), DS header не форк (008). URL из properties — **rule 03**, не ADR.

Не ADR: «в этом тесте опечатка», «поставь JDK 21» (это RAG/rule).

## Каркас (≤ 40 строк)

```markdown
# ADR NNN: короткий заголовок-решение
Статус: предложено | принято | отменено
Контекст: какая развилка.
Решение: что выбрали (1–5 пунктов).
Последствия: что теперь нельзя / что стало проще.
RAG: id чанков, которые держат «как», не «почему».
```

Канон takeaway:

- логин / wrong password: `docs/adr/009-login-401-is-api.md` — UI-текст e2e, 401 JSON уже api;
- screenshot: `docs/adr/005-screenshot-not-layer.md` — не `@Layer`;
- заметка: `docs/adr/006-one-note-not-list.md` (не monorepo `006-allurerc-mjs-ethalon.md`).

Продукт: 007 Spring API-only; 008 DS header не форк. Слои/testid — RAG `be-spring-layers` / `fe-ds-contract`. Факты HTTP — RAG `crud-http`, не ADR.

## Don't

- Дублировать skill целиком внутри ADR.
- Писать ADR на каждый новый тест.
- Менять `@Layer` таблицу без ADR.
