# Домашка: один запрос — и стенд живой

Нужен **Docker Desktop** (запущен). Пустая папка, не этот репозиторий «уже открытый».

1. Cursor или VS Code + Cline: **Open Folder** → новая пустая папка.
2. Вставь промпт ниже в агента. Дождись конца (clone + compose + e2e).
3. Сдай в чат курса: health, Gradle-команда, exit code, путь `allure-results`.

Не коммить. Не гонять prod.

## Промпт

```text
Пустой workspace. Сделай takeaway рабочим локально. Не коммить. Не prod.

1) Clone в текущую папку:
git clone https://github.com/qa-guru/ai-first-student-workspace.git .
Если папка не пустая — clone в подкаталог и работай там.

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

5) Верни: health, команда, exit code, tests run/failed,
путь tests-java-gradle-junit5-allure3-selenide/build/allure-results.
```
