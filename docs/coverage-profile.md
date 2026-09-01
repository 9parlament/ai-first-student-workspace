# Поверхность автоматизации (takeaway)

Ярус × доступ × стек. Как читать — RAG `docs/agent-skills/rag/coverage-access.md`.  
Шаблон под другой контур: `docs/agent-skills/_templates/coverage-profile.md` (после sync).

Это **не** стек продукта целиком и не `layers:` модуля в `matrix.yaml`.

```yaml
product:
  backend:
    stack: java-spring
    access: write
  frontend:
    stack: typescript-react
    access: write

automation:
  unit:
    access: write
    stack: java-spring
    module: backend/java/backend-java-spring
  integration:
    access: write
    stack: java-spring
    module: backend/java/backend-java-spring
  component:
    access: write
    stack: typescript-react
    module: frontend/typescript/frontend-typescript-react
  api:
    access: write
    stack: java-gradle-junit5-selenide
    module: tests/java/tests-java-gradle-junit5-allure3-selenide
  ui:
    access: write
    stack: java-gradle-junit5-selenide
    module: tests/java/tests-java-gradle-junit5-allure3-selenide
  e2e:
    access: write
    stack: java-gradle-junit5-selenide
    module: tests/java/tests-java-gradle-junit5-allure3-selenide
  manual:
    access: write
    stack: java-gradle-junit5-selenide
    module: tests/java/tests-java-gradle-junit5-allure3-selenide
```

`access`: `write` | `read` | `none`.  
Workplace (API C#, UI Python, backend закрыт) — не этот файл; пример в RAG `coverage-access`.
