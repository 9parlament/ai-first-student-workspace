# Agent skills (курс AI-first QA)

Workflows для **Cline** (VS Code + Ollama) в учебном Java/Gradle репо.  
В Cursor monorepo аналог другой: `.cursor/skills/` — студентам не копировать.

Карта пака: [PACK.md](PACK.md) · RAG-диета: [rag/README.md](rag/README.md)  
Листы A4 (skill / rule / RAG / ADR): [lab.qa.guru](https://lab.qa.guru/)

Контракт HTTP CRUD: SSOT `docs/rag/testing/crud-http.md` → диета `rag/crud-http.md`. Generic skills (`qa-write-test`, `be-add-resource`, `fe-add-ui`) таблицу глаголов не держат. Продукт: `be-add-resource` / `fe-add-ui`; пирамида takeaway — `qa-make-full-pyramid` после влитой фичи.

Контракт HTTP CRUD: SSOT `docs/rag/testing/crud-http.md` → диета `rag/crud-http.md`. Generic skills (`qa-write-test`) таблицу глаголов не держат.

## Структура

```text
docs/agent-skills/
├── PACK.md
├── PACK.md
├── adr/                      ← учебные ADR (занятие 4)
├── rag/                      ← дистиллят чанков (id = имя файла)
├── examples/multistack/      ← заполненный takeaway (команды живые)
└── templates/                ← placeholder'ы + skill-stub.md + adr-stub.md
```

После sync в учебный репо skills лежат плоско: `docs/agent-skills/qa-write-test/SKILL.md`.

## Rule vs Skill vs RAG vs ADR

| | Rule | Skill | RAG | ADR |
|---|------|-------|-----|-----|
| Путь | `.clinerules/`, `.cursor/rules/`, `AGENTS.md` | `docs/agent-skills/<name>/SKILL.md` | `docs/agent-skills/rag/` | `docs/adr/` (занятие 4) |
| Роль | лимиты | workflow + DoD | факты (2–4 файла) | почему |
| Загрузка | авто (toggle) | «прочитай SKILL.md» | путь в skill | skill ссылается |

Листы: [00 обзор](https://lab.qa.guru/#00-overview) · [skill](https://lab.qa.guru/#01-skills) · [rule](https://lab.qa.guru/#02-rules) · [RAG](https://lab.qa.guru/#03-rag) · [ADR](https://lab.qa.guru/#04-adr).  
Login без/с: [сценарий](https://lab.qa.guru/#20-login) · [skill](https://lab.qa.guru/#21-login-skill) · [rule](https://lab.qa.guru/#22-login-rule) · [RAG](https://lab.qa.guru/#23-login-rag) · [ADR](https://lab.qa.guru/#24-login-adr).  
Стеки: [только skill](https://lab.qa.guru/#10-stack-skills) → [+ rules](https://lab.qa.guru/#11-stack-skills-rules) → [+ RAG](https://lab.qa.guru/#12-stack-skills-rules-rag) → [полный](https://lab.qa.guru/#13-stack-skills-rules-rag-adr).  
ДЗ: [40 · main → develop](https://lab.qa.guru/#40-homework) · промпты [HOMEWORK.md](../../HOMEWORK.md).  
Лаборатория: [36 · тумблеры слоёв](https://lab.qa.guru/36-login-lab.html).  
Словарь: [50 · AI-стек на LoginTests](https://lab.qa.guru/50-glossary.html).

## Занятие 2

- Преподаватель, второе окно: [teacher-second-workspace.md](../qa-guru/ai-first-qa/lesson-02/teacher-second-workspace.md)
- Сценарий: [scenario-90min.md](../qa-guru/ai-first-qa/lesson-02/scenario-90min.md)
- Worked example: [worked-example-multistack.md](../qa-guru/ai-first-qa/lesson-02/worked-example-multistack.md)

## Занятия 3–4

- [Занятие 3 — RAG + CI](../qa-guru/ai-first-qa/lesson-03/README.md)
- [Занятие 4 — ADR + пирамида](../qa-guru/ai-first-qa/lesson-04/README.md)

Студентам — пути **своего** репо. Не копировать monorepo `projects/…/ethalon/`.
