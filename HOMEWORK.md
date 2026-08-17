# Домашка: один запрос — и стенд живой

Нужен **Docker Desktop** (запущен) и аккаунт GitHub.

1. Форкни https://github.com/qa-guru/ai-first-student-workspace (кнопка **Fork**). Не клонируй `qa-guru` напрямую.
2. Cursor или VS Code + Cline: **Open Folder** → новая пустая папка.
3. Вставь промпт ниже. Дождись конца (clone **твоего форка** + compose + e2e).
4. Сдай в чат курса: URL форка, health, Gradle-команда, exit code, путь `allure-results`.

Не коммить в `qa-guru`. Не гонять prod.

## Промпт

```text
Пустой workspace. Сделай takeaway рабочим локально. Не коммить. Не prod.

1) Не клонируй https://github.com/qa-guru/ai-first-student-workspace.git
   Работать только со СВОИМ форком.

   Если форка ещё нет:
   gh repo fork qa-guru/ai-first-student-workspace --clone=false
   Затем clone форка в текущую папку:
   git clone "https://github.com/$(gh api user --jq .login)/ai-first-student-workspace.git" .
   Если gh нет — спроси мой GitHub login и клонируй
   https://github.com/<login>/ai-first-student-workspace.git
   Если папка не пустая — clone в подкаталог и работай там.

   Проверь: git remote -v → origin = мой форк, не qa-guru.

2) Rules ON. Прочитай AGENTS.md, .cursor/rules/ (или .clinerules/),
docs/agent-skills/qa-smoke-debug/SKILL.md
и только чанки docs/agent-skills/rag/ci-gradle-args.md, cfg-stands.md, allure-attach.md.
Не читай всю папку rag/.

3) В корне репо:
docker compose up -d --build
curl -sf http://localhost:8800/api/health
UI: http://localhost:9821/ (не :9811)

4) Учебный e2e (нет task testE2e, нет @Tag("smoke"), не full suite):
cd tests-java-gradle-junit5-allure3-selenide
./gradlew test -Denv=multistack_ci -DincludeTags=e2e -DexcludeTags=screenshot,mock

5) Верни: URL origin (форк), health, команда, exit code, tests run/failed,
путь tests-java-gradle-junit5-allure3-selenide/build/allure-results.
```
