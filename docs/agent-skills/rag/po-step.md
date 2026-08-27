---
id: po-step
domain: testing
tags: [allure, step]
related: [po-locators, po-fluent, test-negative]
---
# Allure @Step на PO

**id:** `po-step`

Канон: `@Step("…")` на **методах** `LoginPage`, не на классе и не на `@Test`.

```java
@Step("Type username: {username}")
public LoginPage typeUsername(String username) { … }

@Step("Type password")   // не {password} — секрет в Allure
public LoginPage typePassword(String password) { … }
```

## Do

- Глагол + безопасные параметры в тексте шага.
- Один источник шагов: PO `@Step` **или** `Allure.step` в тесте, не оба сразу.

## Don't

- `@Step` / `@Epic` на классе `LoginPage` «как у LoginTests».
- `@Step("Type password: {password}")`.
- Дублировать локаторы в smoke-тесте «чтобы Allure увидел».
