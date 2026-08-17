---
id: remote-selenoid
domain: testing
adr: 002
tags: [selenoid, remote]
---
# Браузер на хабе

**id:** `remote-selenoid`

Профиль `multistack_prod`: `remoteUrl=https://selenoid.qa.guru/wd/hub`. **Креды в git не кладут** — передают `-DremoteUrl=https://user:pass@selenoid.qa.guru/wd/hub` (CI secret / локальный env).

Локальный `multistack_ci`: `remoteUrl` пустой → Chrome на машине.

## Do

- Прод-прогон только с `-Denv=multistack_prod` (и рабочим remoteUrl).
- Capabilities — `selenoid:options` в `TestBase`, не chrome-flags как на local.

## Don't

- `./gradlew test` «на прод» без профиля.
- Коммитить пароль хаба.
