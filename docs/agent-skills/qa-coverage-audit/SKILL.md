---
name: qa-coverage-audit
description: >-
  Оценить покрытие takeaway: @Layer inventory vs flows vs OpenAPI.
  Use when asked for coverage, gaps, or test map.
---

# Оцени покрытие

RAG: `test-pyramid`, `test-layers`, `test-taxonomy`, `test-api-layer`.

## When

- «какое покрытие», «чего не хватает», «карта тестов»

## Do not

- Путать line coverage JaCoCo с пирамидой
- Предлагать «добавить e2e на всё»
- Менять код в этом task (план — да, реализация — `qa-pyramid-plan` / `qa-write-test`)

## Steps

1. Inventory классов в `tests/e2e`, `tests/api`, `tests/manual`, `tests/testinfra` (+ backend `src/test`, если есть).
2. Таблица: класс × `@Layer` × `@Tag` × сценарий (DisplayName).
3. Flows продукта (минимум): login / register / logout / home health+items / auth API.
4. Сверить с `tests/api/AuthApiTests` vs `tests/e2e/LoginTests` — где дубль, где дыра.
5. Screenshot/mock — отдельно как **slice**, не как недостающий ярус.

## Формат ответа

| Сценарий | api | e2e | manual | Дыра? |
|----------|:---:|:---:|:------:|-------|
| login valid | | | | |
| login wrong password | | | | |
| register | | | | |
| home items | | | | |

Плюс 3 приоритетных пробела (ярус + почему не e2e).

## DoD

- [ ] Inventory не «у нас всё покрыто» без таблицы
- [ ] Slice ≠ слой
- [ ] Нет правок кода
- [ ] 3 приоритета с ярусом

## Example prompt

```text
Прочитай docs/agent-skills/qa-coverage-audit/SKILL.md и test-pyramid.
Оцени покрытие модуля tests-java-…. Таблица + 3 дыры. Код не меняй.
```
