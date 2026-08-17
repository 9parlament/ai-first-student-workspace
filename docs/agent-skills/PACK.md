# Пак QA skills / rules / RAG (AI-first)

Учебный комплект под takeaway  
[java_spring-typescript_react-java_selenide](https://github.com/autotests-ai/java_spring-typescript_react-java_selenide).

Копирование в demo-workspace: [sync-to-workspace.sh](sync-to-workspace.sh).  
Второе окно преподавателя: [lesson-02/teacher-second-workspace.md](../qa-guru/ai-first-qa/lesson-02/teacher-second-workspace.md).

## Слои

| Слой | Где | Роль |
|------|-----|------|
| Rules | `.clinerules/*.md`, `AGENTS.md` | лимиты |
| Skills | `docs/agent-skills/<name>/SKILL.md` | workflow + DoD |
| RAG | `docs/agent-skills/rag/<id>.md` | факты проекта (2–4 файла на задачу) |
| ADR | цитата в skill (модуль 3 — писать свои) | почему |

## Skills

| Skill | Промпт | Модуль | Файлы |
|-------|--------|--------|-------|
| `qa-smoke-debug` | smoke e2e + Allure + flaky | 1 · зачёт | [example](examples/multistack/qa-smoke-debug/SKILL.md) · [template](templates/qa-smoke-debug/SKILL.md) |
| `qa-write-test` | разработай автотест | 1–8 | [example](examples/multistack/qa-write-test/SKILL.md) · [template](templates/qa-write-test/SKILL.md) |
| `qa-review-framework` | ревью фреймворка | 1 | [example](examples/multistack/qa-review-framework/SKILL.md) |
| `qa-bootstrap-framework` | фреймворк «с нуля» = takeaway + чеклист | 8 | [example](examples/multistack/qa-bootstrap-framework/SKILL.md) |
| `qa-coverage-audit` | оцени покрытие | 8 / 10 | [example](examples/multistack/qa-coverage-audit/SKILL.md) |
| `qa-pyramid-plan` | 100% пирамида: план + один ярус | 10 | [example](examples/multistack/qa-pyramid-plan/SKILL.md) |
| `qa-run-stand` | прогон на pipeline / stage / prod | 10 | [example](examples/multistack/qa-run-stand/SKILL.md) |

Домашка: пустой workspace → [один промпт](../../HOMEWORK.md) (`git clone` + compose + e2e). Не семь чатов.

## Rules (example)

| Файл | Лимит |
|------|--------|
| [01-qa-java-gradle.md](examples/multistack/clinerules/01-qa-java-gradle.md) | e2e-команда, не full suite |
| [02-git-safety.md](examples/multistack/clinerules/02-git-safety.md) | нет commit без OK |
| [03-env-and-stand.md](examples/multistack/clinerules/03-env-and-stand.md) | pipeline / stage / prod, всегда `-Denv` |
| [04-one-task-one-layer.md](examples/multistack/clinerules/04-one-task-one-layer.md) | один task = один ярус |

## Команда e2e (канон takeaway)

```bash
cd tests-java-gradle-junit5-allure3-selenide
./gradlew test -Denv=multistack_ci -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

В этом стеке нет Gradle-task `testE2e` и нет `@Tag("smoke")`. Учебный «smoke» = тег `e2e` минус screenshot/mock.

CI takeaway: `.github/workflows/ci.yml`. Прод-стенд этого стека: [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) (`-Denv=multistack_prod`), не матрица `/stack/…`.
