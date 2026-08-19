---
name: qa-make-full-pyramid
description: >-
  Закрыть уже влитую фичу по ярусам unit → integration → component → api → e2e → manual.
  Один вызов = один ярус; после яруса STOP. Не заменяет qa-write-test / qa-coverage-audit.
---

# Полная пирамида — один ярус за вызов

Фича **уже влита**. Этот skill не пишет продукт и не заменяет:
`qa-coverage-audit` (карта), `qa-pyramid-plan` (план + одна дыра продукта),
`qa-write-test` (как писать api/e2e).

«100% пирамиды» = каждый сценарий фичи на **своём** `@Layer` (RAG `test-pyramid`).
Не 100% строк JaCoCo (`quality-gates`). Не e2e на весь CRUD. Slice ≠ слой.

## When

- «закрой пирамиду по заметке», «ярус unit/api/e2e…», «следующий ярус»
- После влитой фичи, не вместо реализации

## Do not

- Реализовывать фичу (нет заметки в коде → STOP, сказать человеку)
- Два яруса в одном вызове; «добить всё»
- Подменять `qa-write-test` / `qa-coverage-audit`
- E2e на весь CRUD; `@Layer("screenshot")`; smoke как ярус
- Delete/drop на prod без явного OK (`cfg-stands`)
- `localhost` / prod URL в Java
- Чинить чужие тесты «заодно»
- Commit без OK

## RAG (на вызов — 2–4 id, не все сразу)

Каталог: `test-pyramid` · `test-layers` · `test-api-layer` · `cfg-stands` · `adr-when` · `quality-gates`.

| Ярус | Читать |
|------|--------|
| unit | `test-pyramid`, `quality-gates`, `test-layers` |
| integration | `test-pyramid`, `test-layers`, `cfg-stands` |
| component | `test-pyramid`, `test-layers` |
| api | `test-api-layer`, `test-layers`, `cfg-stands` |
| e2e | `test-pyramid`, `test-layers`, `cfg-stands` (+ `qa-write-test` и его RAG) |
| manual | `test-pyramid`, `test-layers`, `adr-when` |

ADR фичи: `docs/adr/006-one-note-not-list.md`. Slice: `docs/adr/005-screenshot-not-layer.md`.

## Якоря (образец слоя, не дописывать чужой фиче)

| `@Layer` | Класс / файл | Прогон яруса |
|----------|--------------|--------------|
| unit | `backend-java-spring/…/service/ItemServiceTest.java` | `cd backend-java-spring && ./gradlew test jacocoTestReport jacocoTestCoverageVerification -DexcludeTags=integration` |
| integration | `backend-java-spring/…/integration/AuthLifecycleIntegrationTest.java` | `cd backend-java-spring && ./gradlew test -DincludeTags=integration` |
| component | `frontend-typescript-react/src/test/pages/HomePage.test.tsx` | `cd frontend-typescript-react && npm test -- --coverage` |
| api | `tests-java-gradle-junit5-allure3-selenide/…/tests/api/AuthApiTests.java` | `cd tests-java-gradle-junit5-allure3-selenide && ./gradlew test -Denv=ci -DincludeTags=api` |
| e2e | `…/tests/e2e/LoginTests.java` | `cd tests-java-gradle-junit5-allure3-selenide && ./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot,mock` |
| manual | `…/tests/manual/ExploratoryManualTests.java` | `cd tests-java-gradle-junit5-allure3-selenide && ./gradlew test -Denv=ci -DincludeTags=manual` |

Изолированно: тот же `-Denv` / tags + `-Dtest=Class#method` (api/e2e) или точечный класс backend/Vitest.

Порядок ярусов, если человек не назвал: **unit → integration → component → api → e2e → manual**.

## Steps

1. Фича влита? Нет → STOP. Не кодить продукт.
2. Ярус = тот, что назвал человек, иначе первый пустой в порядке выше. Rule: один task = один `@Layer`.
3. Прочитай **этот** SKILL и **2–4** RAG из таблицы яруса.
4. Api/e2e — пиши по `qa-write-test` (PO/клиент, tags, стенды). Unit/integration/component/manual — по якорю слоя.
5. Стенды: pipeline (`-Denv=ci`) / stage / prod. Delete — pipeline/stage; prod только с OK и отдельным `@Tag`.
6. Прогон **только этого** яруса (команда из таблицы, лучше точечный `-Dtest`).
7. Строка в `docs/lessons/note-crud-pyramid.md` (сценарий × ярус, лог фазы, exit code).
8. **STOP.** Ждать «следующий ярус». Не начинать соседний слой.

## DoD

- [ ] Фича уже влита (этот skill её не писал)
- [ ] Ровно один `@Layer`; slice не назван ярусом
- [ ] 2–4 RAG, не вся папка
- [ ] Стенды названы; delete на prod не без OK
- [ ] Прогон яруса с `-DincludeTags` / exclude integration / Vitest; exit code в ответе
- [ ] Живой отчёт обновлён
- [ ] Нет commit без OK
- [ ] Следующий ярус не начат

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-make-full-pyramid/SKILL.md
и 2–4 RAG текущего яруса. Фича заметки уже влита.
Ярус: unit. По якорю ItemServiceTest. Не коммить. После яруса STOP.
```
