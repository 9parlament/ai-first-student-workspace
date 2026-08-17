---
id: po-locators
domain: testing
adr: 002
tags: [selenide, locators]
---
# Селекторы только в PO

**id:** `po-locators`

Канон: `pages/LoginPage.java` — `data-testid`.

```java
private final SelenideElement loginInput = $("[data-testid='login-input']");
```

## Do

- `private final` локаторы в Page Object.
- В приложении — стабильный `data-testid`.

## Don't

- `$(".btn")` / xpath в `*Tests`.
- Копировать локатор в два PO.
