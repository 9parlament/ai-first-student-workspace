---
id: po-locators
domain: testing
tags: [selenide, locators]
related: [po-fluent, po-step]
---
# Селекторы только в PO

**id:** `po-locators`

Канон: `pages/LoginPage.java` — `data-testid`.

```java
private final SelenideElement loginInput = $("[data-testid='login-input']");
private final SelenideElement errorMessage = $("[data-testid='error-message']");
```

## Do

- `private final` локаторы в Page Object.
- В приложении — стабильный `data-testid`.

## Don't

- `$(".btn")` / xpath в `*Tests`.
- Копировать локатор в два PO.
