---
id: test-api-layer
domain: testing
adr: 004
tags: [api, rest-assured]
---
# API слой

**id:** `test-api-layer`

Канон: `api/ApiTestBase.java`, `api/AuthApiClient.java`, `tests/api/AuthApiTests.java`.  
`@Layer("api")` + `@Tag("api")`. Браузера нет.

```bash
./gradlew test -Denv=multistack_ci -DincludeTags=api
```

## Do

- Новый endpoint → класс в `tests/api/`, assert через Rest Assured.
- Схема: `src/test/resources/schemas/`.

## Don't

- `@Layer("api")` + `TestBase` / Selenide.
- Проверять JSON-контракт логина только кликами в UI.
