---
id: test-taxonomy
domain: testing
adr: 002
tags: [allure, epic, feature, tag]
---
# Allure labels

**id:** `test-taxonomy`

Канон на классе `LoginTests`: `@Epic("Authentication")`, `@Feature("Login")`, `@Layer("e2e")`. На методе — `@Tag("e2e")` + `positive` / `negative`.

## Do

- Epic / Feature на **классе**.
- `@DisplayName` человекочитаемый — его видно в Allure и в `-Dtest=`.

## Don't

- Мешать epic Home и Authentication в одном классе без причины.
