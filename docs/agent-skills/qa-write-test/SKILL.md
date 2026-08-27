---
name: qa-write-test
description: >-
  Написать автотест по канону takeaway: слой, PO, tags, Allure.
  Use when asked to add e2e/api test, cover a scenario, or copy LoginTests.
---

# Разработай автотест

## When

- «напиши e2e на …», «добавь negative login», «покрой API login»

## RAG (2–4 id, не всю папку)

| Задача | Читай |
|--------|--------|
| UI / PO | `po-locators` · `po-fluent` · `po-step` |
| negative login | `po-locators` · `po-step` · `test-negative` · `cfg-stands` |
| JSON-контракт | `test-api-layer` · `cfg-stands` |

Для промпта «неуспешный логин с неправильным паролем» — **вторая строка** (ровно 4).  
Развилка 401 JSON vs текст на форме — ADR `docs/adr/009-login-401-is-api.md`, не этот skill.

## Do not

- CSS/xpath в классе `*Tests`
- Новый `ChromeDriver` / setup в тесте
- Подменять `qa-make-full-pyramid` / продукт (`be-add-resource` / `fe-add-ui`)
- На `main` нет `/api/note` — не выдумывать. **Дыра** — если фича в дереве, а слота нет

Commit, URL в Java, всегда `-Denv`, один task = один ярус — **rule**, не этот файл.  
Api vs e2e на 401 — **ADR 009**, не решай в чате.

## Якоря

| Слой | Образец |
|------|---------|
| e2e | `tests/e2e/LoginTests`, `pages/LoginPage` (`data-testid`) |
| api | `tests/api/AuthApiTests`, `api/AuthApiClient` |
| fluent happy | `loginPage.openPage().fillAndSubmitForm("user1", "password1")` |
| fluent negative | `typeUsername` → `typePassword` → `submitExpectingError` (чанк `test-negative`) |

## Steps

1. Один `@Layer`. Логин: текст на форме vs 401 JSON — ADR 009.
2. Стенды (чанк `cfg-stands`): pipeline / stage / prod? Сиды есть на всех? URL только из config.
3. Есть PO/клиент? Расширь. Нет — локаторы в `pages/`, не в тесте.
4. Класс: `@Layer`, `@Epic`, `@Feature`, `@DisplayName`. Метод: `@Tag` яруса + `positive`/`negative`.
5. Прогон только этого теста на **pipeline-профиле** (локальный compose):

```bash
cd tests/java/tests-java-gradle-junit5-allure3-selenide
# e2e
./gradlew test -Denv=ci -DincludeTags=e2e -Dtest=LoginTests#<method>
# api
./gradlew test -Denv=ci -DincludeTags=api -Dtest=AuthApiTests#<method>
```

6. В ответе: слой, **на каких стендах поедет**, команда, exit code. Оставшиеся ярусы фичи — **Дыра**, не писать их сейчас.

## DoD

- [ ] Слой выбран явно
- [ ] Названы стенды: pipeline / stage / prod
- [ ] Локаторы не в тесте
- [ ] `@Step` на PO или api-шаги в отчёте
- [ ] Изолированный Gradle-прогон с `-Denv=ci` (или явно другой env)
- [ ] Живые дыры фичи названы (не закрыты в этом task)

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-write-test/SKILL.md
и чанки po-locators, po-step, test-negative, cfg-stands.
Добавь автотест на неуспешный логин с неправильным паролем.
Укажи pipeline/stage/prod.
```
