Загрузить контекст репо: $ARGUMENTS

1. Прочитать <repo>/CLAUDE.md через Read — стек, команды, архитектура, ограничения.

2. mcp__github__list_commits (repo: SilentCare-so/<repo>, limit 10) — последние коммиты.

3. mcp__github__list_pull_requests (repo: SilentCare-so/<repo>, state: open) — открытые PR.

4. Краткое резюме: что за репо, что сейчас в работе, на что обратить внимание.

Если репо не указан в $ARGUMENTS — спросить какой репо загрузить.
