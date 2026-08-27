---
id: po-fluent
domain: testing
tags: [selenide, pageobject]
related: [po-locators, po-step, test-negative]
---
# Fluent Page Object

**id:** `po-fluent`

Канон: `pages/LoginPage.java` + `tests/e2e/LoginTests.shouldLoginWithValidCredentials`.

```java
loginPage.openPage()
        .fillAndSubmitForm("user1", "password1")
        .shouldHaveWelcomeMessage("Welcome, user1!");
```

## Do

- Методы PO возвращают `this` или следующую страницу (`HomePage`).
- Assert видимости — `should*` с понятным именем.

## Don't

- `void clickLogin()` без возврата страницы.
- Assert в PO без `@Step`.
- Sad path логина через `fillAndSubmitForm` — он ждёт `HomePage`. Чанк `test-negative`.
