# Agent skills (курс AI-first QA)

Workflows для **Cline** (VS Code + Ollama) в учебном Java/Gradle репо.  
В Cursor monorepo аналог другой: `.cursor/skills/` — студентам не копировать.

Карта пака: [PACK.md](PACK.md) · RAG-диета: [rag/README.md](rag/README.md)  
Demo-workspace: [sync-to-workspace.sh](sync-to-workspace.sh)

## Структура

```text
docs/agent-skills/
├── PACK.md
├── rag/                      ← дистиллят чанков (id = имя файла)
├── examples/multistack/      ← заполненный takeaway (команды живые)
└── templates/                ← placeholder'ы + skill-stub.md
```

После sync в учебный репо skills лежат плоско: `docs/agent-skills/qa-write-test/SKILL.md`.

## Rule vs Skill vs RAG vs ADR

| | Rule | Skill | RAG | ADR |
|---|------|-------|-----|-----|
| Путь | `.clinerules/`, `AGENTS.md` | `docs/agent-skills/<name>/SKILL.md` | `docs/agent-skills/rag/` | цитата / модуль 3 |
| Роль | лимиты | workflow + DoD | факты (2–4 файла) | почему |
| Загрузка | авто (toggle) | «прочитай SKILL.md» | путь в skill | skill ссылается |

## Занятие 2

- Преподаватель, второе окно: [teacher-second-workspace.md](../qa-guru/ai-first-qa/lesson-02/teacher-second-workspace.md)
- Сценарий: [scenario-90min.md](../qa-guru/ai-first-qa/lesson-02/scenario-90min.md)
- Worked example: [worked-example-multistack.md](../qa-guru/ai-first-qa/lesson-02/worked-example-multistack.md)

Студентам — пути **своего** репо. Не копировать monorepo `projects/…/ethalon/`.
