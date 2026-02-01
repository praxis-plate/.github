# AGENTS

Workspace-wide rules for this repository root that contains multiple projects:
- praxis_flutter (Flutter app)
- praxis_server (Serverpod server)
- research-paper (symlink outside repo; treat as read-only unless explicitly asked)

Codex applies the closest AGENTS.md to the files being edited. Prefer project-specific rules in:
- praxis_flutter/AGENTS.md
- praxis_server/AGENTS.md

## Language policy (documentation and comments)

- All documentation and comments MUST be written in English only.
- If you encounter existing non-English comments, do not translate them unless the task explicitly requests it.
- New comments introduced as part of a change MUST follow this rule.

## Safety & scope

- Do not edit generated build artifacts or caches (e.g., build/, .dart_tool/) unless the task explicitly requires it.
- Do not modify files outside this repository root. The `research-paper` entry is a symlink; treat it as read-only unless the user explicitly requests changes there.

## Dart/Flutter SDK (FVM)

This workspace uses FVM.

- Do not change pinned FVM/Flutter/Dart versions unless explicitly requested.
- Always invoke Dart/Flutter through FVM to match the pinned SDK:
  - Prefer `fvm dart ...` and `fvm flutter ...`
  - For tools that call `dart`/`flutter` indirectly, use `fvm exec <command>`

Examples:
- `fvm dart --version`
- `fvm flutter pub get`
- `fvm exec dart run build_runner build`

## Quick commands (run from the target project directory)

- praxis_flutter:
  - `fvm flutter pub get`
  - `fvm dart format .`
  - `fvm flutter analyze`
  - `fvm flutter test`

- praxis_server:
  - `fvm dart pub get`
  - `fvm dart format .`
  - `fvm dart analyze`
  - `fvm dart test` (or the project’s standard server test command)

## Change strategy

- Prefer minimal, enterprise-style changes: modify existing logic rather than rewriting or reshaping it.
- Keep changes scoped to the task. If refactoring is needed, isolate it and justify it.
- Order methods by call flow where it improves readability (Clean Code style).

## Definition of Done

1) Formatting applied (`dart format` where relevant) and produces no further diff
2) Static analysis passes (`dart analyze` / `flutter analyze` as appropriate)
3) Tests for the affected project pass
4) No cross-layer leakage or ad-hoc shortcuts introduced
5) No unrelated changes

## Review guidelines

- Verify project boundaries (do not mix client/server concerns).
- Check for unnecessary dependency additions or architecture reshaping.
- Ensure error handling is explicit and test coverage is adequate for business logic changes.
- Prefer clarity over cleverness; avoid ambiguous naming and hidden control flow.
- Ensure any newly added comments/documentation are in English only.
