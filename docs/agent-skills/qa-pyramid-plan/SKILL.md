---
name: qa-pyramid-plan
description: >-
  План 100% пирамиды и реализация одного недостающего яруса.
  Use when asked for pyramid plan or to fill a missing layer.
---

# 100% пирамида — план и один шаг

RAG: `test-pyramid`, `test-layers`, `test-api-layer`, `cfg-stands`.  
Идея ADR 005: **visual/screenshot — slice, не `@Layer`**. Полный ADR — модуль 3; здесь только это правило.

«100%» = сценарии на **своих** ярусах, не 100% строк кода.

## When

- «план пирамиды», «довёл до 100%», «куда класть этот кейс»

## Do not

- Добавлять e2e вместо api
- Вводить `@Layer("screenshot")`
- Реализовывать все дыры в одном task (один ярус / один тест)

## Steps

1. Возьми таблицу из `qa-coverage-audit` (или собери коротко).
2. План: для каждой дыры — ярус + класс-якорь + **на каких стендах** (pipeline / stage / prod).
3. Согласуй с человеком **одну** реализацию.
4. Пиши по `qa-write-test` (PO/api-клиент, tags).
5. Прогон только этого слоя.

Примеры правильного слота:

| Дыра | Куда |
|------|------|
| JSON login 401 | `AuthApiTests`, не новый UI-клик |
| Текст ошибки на форме | `LoginTests` + PO, уже есть wrong password |
| Чеклист exploratory | `tests/manual`, `@Manual` |

## DoD

- [ ] План таблицей (дыра → ярус)
- [ ] Не больше одного нового теста без OK
- [ ] Прогон с правильным `-DincludeTags`
- [ ] Screenshot не назван ярусом

## Example prompt

```text
Прочитай docs/agent-skills/qa-pyramid-plan/SKILL.md и test-pyramid.
План пирамиды по takeaway. Реализуй только если я скажу какой ярус.
Не коммить.
```
