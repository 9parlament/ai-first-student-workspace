---
id: test-negative
domain: testing
adr: 009
tags: [negative, login]
related: [po-locators, po-step, cfg-stands, testdata-user]
---
# Negative login

**id:** `test-negative`

Канон: `tests/e2e/LoginTests#shouldShowErrorWhenPasswordIsWrong`.

```java
loginPage.openPage()
        .typeUsername("user1")
        .typePassword("wrongpassword")
        .submitExpectingError()
        .shouldHaveErrorMessage("Wrong login or password");
```

Текст ошибки — константа в тесте (`WRONG_CREDENTIALS_MESSAGE`).  
`fillAndSubmitForm` сюда нельзя: он ждёт `HomePage`, а не сообщение на форме.

Empty username / empty password — те же `type*` + `submitExpectingError`, другие константы в `LoginTests`. Empty username: `typePassword("password1")` — литерал длины, не `UserBuilder` (чанк `testdata-user`).

## Do

- Один ожидаемый текст на сценарий.
- `@Tag("negative")` рядом с `@Tag("e2e")`. Не `@Tag("smoke")` на этот метод.

## Don't

- Inline `$("input")` в negative-тесте.
- «Invalid credentials» / «Unauthorized» — в UI другая строка.
- Собирать `User` для кейса, где пользователя нет (чанк `testdata-user`).
