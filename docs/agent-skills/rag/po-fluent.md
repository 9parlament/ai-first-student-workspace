---
id: po-fluent
domain: testing
adr: 002
tags: [selenide, pageobject]
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
