# 001 - Top-level README for example inventory

## Decision Intent Log

ID: DI-001-20260428-123034
Date: 2026-04-28 12:30:34
Status: active
Decision: Create a root `README.md` that describes each bundled Arduino example, each ESP-IDF example, and the prebuilt firmware artifact, using local repo inspection and Waveshare setup guides as background.
Intent: Give the repository a single onboarding document that helps a reader understand what each example does, what inputs it needs, and how to run it without first reverse-engineering every sketch and project.
Constraints: Touch only `README.md`, `TODO/TODO.md`, and `TODO/001-top-level-readme.md`; preserve vendor example names and directory structure; do not modify source code; do not run build, flash, or hardware tests.
Affects: `README.md`, `TODO/TODO.md`, `TODO/001-top-level-readme.md`

## Decision Lock

- `D-001` Create a persistent root `README.md` as the repo index.
- `D-002` Document all Arduino, ESP-IDF, and Firmware examples.
- `D-003` Use local files plus Waveshare setup docs as background only.
- `D-004` Reuse existing folder names as README section labels and example identifiers.
- `D-005` Create `TODO/TODO.md` as the required task index.
- `D-006` Create `TODO/001-top-level-readme.md` as the task-specific decision log.
- `D-007` Avoid runtime writes outside the three approved documentation paths.

## Subtasks

- [x] 001.1 Inventory the Arduino, ESP-IDF, and Firmware example sets.
- [x] 001.2 Review the local per-example notes and entry files.
- [x] 001.3 Review Waveshare Arduino and ESP-IDF environment setup guidance.
- [x] 001.4 Write `README.md` with a top-level usage guide.
- [x] 001.5 Review the new docs for scope and consistency.
