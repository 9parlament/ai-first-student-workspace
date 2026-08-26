---
paths:
  - "tests/java/tests-java-gradle-junit5-allure3-selenide/**"
---

# takeaway — e2e / api defaults

Модуль: `tests/java/tests-java-gradle-junit5-allure3-selenide/`.

## E2e (учебный smoke)

```bash
cd tests/java/tests-java-gradle-junit5-allure3-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

- Нет Gradle-task `testE2e`. Срез занятия = `@Tag("e2e")` минус screenshot/mock.
- `@Tag("smoke")` на узких методах — prod slice, не замена команды выше (ярус vs slice — ADR 005).
- Не `./gradlew test` без `-DincludeTags` для задачи «smoke / e2e».
- Всегда `-Denv=` (pipeline `ci` / stage / prod). URL в Java — rule 03.
- Один метод (`-Dtest=`) — skill `qa-write-test` / flaky — `qa-smoke-debug`. Allure — тот же `qa-smoke-debug`.

## API

```bash
./gradlew test -Denv=ci -DincludeTags=api
```

## Новый продукт без яруса

Эндпоинт / панель в коде, а в этом модуле нет api и/или e2e по слоту — в ответе **Дыра**. Не закрывать unit/JaCoCo отсюда. Пирамида — `qa-make-full-pyramid`, один ярус.

## Skills

`docs/agent-skills/qa-smoke-debug/SKILL.md` и соседние skills в `docs/agent-skills/`.
