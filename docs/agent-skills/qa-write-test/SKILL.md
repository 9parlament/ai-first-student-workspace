---
name: qa-write-test
description: >-
  Написать автотест по канону takeaway: слой, PO, tags, Allure.
  Use when asked to add ui/e2e/api test, cover a scenario, or copy LoginTests.
---

# Разработай автотест

RAG (прочитай до кода): `po-fluent`, `po-locators`, `po-step`, `test-negative`, `testdata-user`, `test-taxonomy`, `test-layers`, `cfg-stands`.

## When

- «напиши e2e на …», «покрой header на mock», «добавь negative login», «покрой API login»

## Do not

- CSS/xpath в классе `*Tests`
- Новый `ChromeDriver` / setup в тесте
- E2e на JSON-контракт, если место в `tests/api`
- `localhost` / prod URL / пароль хаба в Java
- Деструктивный сценарий на prod без OK / без ADR фичи с фабрикой (`cfg-stands`)
- Commit без OK

## Якоря

| Слой | Образец |
|------|---------|
| e2e | `tests/e2e/LoginTests`, `pages/LoginPage` (`data-testid`) |
| ui | `tests/ui/HeaderTests` / `LoginFormTests` — chrome на `-Denv=mock`; header через `BasePage.header` |
| api | `tests/api/AuthApiTests`, `api/AuthApiClient` |
| fluent e2e | `loginPage.openPage().fillAndSubmitForm("user1", "password1")` — сид литералами, чанк `testdata-user` |
| fluent ui | `loginPage.openPage().header.shouldHaveLangLabel("EN")` |

## Steps

1. Выбери **один** `@Layer` (чанк `test-layers`). Chrome на стабе — `ui`. Сквозной путь через живой `/api` — `e2e`. JSON-контракт — `api`.
2. **Стенды (чанк `cfg-stands`):** этот тест поедет на pipeline (`ci`), stage (`stage`) и/или prod (`prod`)? Данные (сиды) есть на всех? Сиды на prod не сносить. Фабрика+teardown на prod — только если ADR фичи. URL только из config. Контракт новой фичи — её RAG, не этот skill.
3. Есть PO/клиент? Расширь его. Нет — создай локаторы в `pages/` (общий chrome — `pages/components/`), не в тесте.
4. Класс: `@Layer`, `@Epic`, `@Feature`, `@DisplayName`. Метод: `@Tag` яруса + `positive`/`negative`.
5. Прогон только этого теста на профиле слоя (`mock` для ui, `ci` для e2e/api):

```bash
cd tests/java/tests-java-gradle-junit5-allure3-selenide
# e2e
./gradlew test -Denv=ci -DincludeTags=e2e -Dtest=LoginTests#<method>
# ui
./gradlew test -Denv=mock -DincludeTags=ui -Dtest=HeaderTests#<method>
# api
./gradlew test -Denv=ci -DincludeTags=api -Dtest=AuthApiTests#<method>
```

6. В ответе: слой, **на каких стендах поедет**, команда, exit code. Не коммитить.

## DoD

- [ ] Слой выбран явно
- [ ] Названы стенды: mock / pipeline / stage / prod (что да / нет)
- [ ] Нет URL и секретов в тесте
- [ ] Локаторы не в тесте
- [ ] `@Step` на PO или api-шаги в отчёте
- [ ] Изолированный Gradle-прогон с `-Denv=ci` (или явно другой env)
- [ ] Нет commit

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-write-test/SKILL.md
и чанки po-fluent, po-step, test-negative, cfg-stands.
Добавь e2e по образцу LoginTests#shouldShowErrorWhenPasswordIsWrong
(не дублируй существующий метод). Укажи pipeline/stage/prod. Не коммить.
```
