# ADR 009 (учебный): wrong password — UI-текст e2e, 401 JSON — api

**Статус:** принято  
**Дата:** 2026-08-25

## Контекст

Один сценарий «неверный пароль» — две поверхности: читаемый текст на форме и HTTP 401 + JSON. В каждом чате хочется закрыть JSON кликом или assert статуса в DOM. Так контракт закрывают браузером, хотя `AuthApiTests#loginWithInvalidPassword` уже есть.

## Решение

1. Текст на форме → `LoginTests#shouldShowErrorWhenPasswordIsWrong`, `@Layer("e2e")`.
2. Контракт 401 + schema → уже `AuthApiTests#loginWithInvalidPassword`, `@Layer("api")`. Новый браузерный тест под HTTP-статус не пишем.

## Последствия

- Не `$("pre").shouldHave(text("401"))` и не e2e, который ищет JSON в UI.
- Не решать api vs e2e на логин в чате — этот файл.
- Селекторы, текст ошибки, fluent — RAG, не этот ADR.

## RAG

`test-negative` · `test-api-layer`

Не дублировать skill. Не писать ADR на каждый новый метод `LoginTests`.  
Screenshot как slice — другой ADR: `005-screenshot-not-layer`.
