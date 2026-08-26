# ADR 005 (учебный): screenshot — slice, не слой

**Статус:** принято  
**Дата:** 2026-08-19

## Контекст

Хочется «ярус визуальных тестов» рядом с api/e2e. В CI уже есть compare PNG (mock / stage). Если завести `@Layer("screenshot")`, сломается маппинг TestOps и пирамида: пиксельный diff — это тот же браузерный сценарий, другой **отбор**.

## Решение

1. Классы `*ScreenshotTests` остаются `@Layer("e2e")`.
2. Отбор: `@Tag("screenshot")` + `-Denv=mock` или `stage` + job `ui-mock-tests` / stage screenshots.
3. `@Tag("smoke")` — тоже slice (узкий прод), не ярус.
4. Mock UI (`-Denv=mock`) — slice, не api-слой.

## Последствия

- Новый визуальный кейс ≠ новый `@Layer`.
- «100% пирамида» не требует screenshot на каждый flow.
- Полный ADR школы (monorepo) студентам не копировать — этот файл достаточен.

## RAG

`test-pyramid` · `test-layers` · `ci-github-actions`
