---
id: tms-meta
domain: testing
tags: [allure, testops, jira, tms]
related: [test-taxonomy, test-layers]
---
# Мета-теги TMS

**id:** `tms-meta`

Связка автотеста с TestOps / Jira — аннотации, не комментарий в PR.

| Аннотация | Зачем | Пример takeaway |
|-----------|--------|-----------------|
| `@AllureId("46592")` | стабильный id кейса TestOps | `LoginFormTests` |
| `@Issue("MUL-2")` | ключ Jira (story/bug) | тот же метод |
| `@Epic` / `@Feature` | иерархия в Allure = словарь проекта | `Authentication` / `Login` |
| `@Layer("e2e")` | Test Layer в TestOps = **E2E Tests** | не «UI Tests» |
| `@Tag("smoke")` | узкий slice, не ярус | `HomeTests`, login valid |

Школьный контур (когда выдадут доступы): TestOps [allure.qa.guru](https://allure.qa.guru) · Jira [jira.qa.guru](https://jira.qa.guru). Пока нет проекта — **не** выдумывать чужие id.

## Do

- Один primary `@Issue` на тест.
- `@AllureId` только существующий (или явный «создать кейс → вписать»).
- Слой в TestOps маппится с `@Layer`, не с именем класса.

## Don't

- Копировать `MUL-2` / `46592` в свой форк как «магические константы», если это не ваш контур.
- Класть токен TestOps в git.
- Путать `@Tag("smoke")` с Test Layer.
