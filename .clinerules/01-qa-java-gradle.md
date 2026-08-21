---
paths:
  - "**/*Tests.java"
  - "**/*Test.java"
  - "**/tests/**"
  - "**/build.gradle"
---

# takeaway — e2e / api defaults

Модуль: `tests/java/tests-java-gradle-junit5-allure3-selenide/`.

## E2e (учебный smoke)

```bash
cd tests/java/tests-java-gradle-junit5-allure3-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

- Нет Gradle-task `testE2e`. Срез занятия = `@Tag("e2e")` минус screenshot/mock.
- `@Tag("smoke")` на узких методах — prod slice, не ярус и не замена команды выше.
- Не `./gradlew test` без `-DincludeTags` для задачи «smoke / e2e».
- Всегда `-Denv=` (pipeline `ci` / stage / prod). URL не в тестах.

## Один тест

```bash
./gradlew test -Denv=ci -DincludeTags=e2e -Dtest=HomeTests
./gradlew test -Denv=ci -DincludeTags=e2e \
  -Dtest=LoginTests#shouldShowErrorWhenPasswordIsWrong
```

## API

```bash
./gradlew test -Denv=ci -DincludeTags=api
```

## Allure

- Results: `tests/java/tests-java-gradle-junit5-allure3-selenide/build/allure-results`
- Report: `npx allure serve build/allure-results` (из модуля тестов, после `npm ci`)

## Skills

`docs/agent-skills/qa-smoke-debug/SKILL.md` и соседние skills в `docs/agent-skills/`.
