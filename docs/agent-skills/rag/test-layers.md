---
id: test-layers
domain: testing
adr: 002
tags: [layer, allure, gradle]
related: [test-pyramid, ci-gradle-args]
---
# @Layer → тег → Gradle

**id:** `test-layers`

В takeaway ключ `@Layer` и `@Tag` на классе/методе совпадают по имени яруса.

| `@Layer` | `@Tag` | Команда |
|----------|--------|---------|
| e2e | `e2e` | `./gradlew test -Denv=multistack_ci -DincludeTags=e2e -DexcludeTags=screenshot,mock` |
| api | `api` | `./gradlew test -Denv=multistack_ci -DincludeTags=api` |
| manual | `manual` | `./gradlew test -Denv=multistack_ci -DincludeTags=manual` |
| harness | `harness` | `./gradlew test -Denv=multistack_ci -DincludeTags=harness` |

Browser smoke в Allure/TestOps — слой **E2E Tests**, не «UI Tests».

## Don't

- Вешать `@Tag("smoke")`, если в проекте среза нет — здесь срез e2e.
- `@Tag("api")` + `@Tag("e2e")` на одном методе.
