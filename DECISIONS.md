# UnLondon — Decisions

This is an index of significant decisions already documented in the existing project files. The original wording and detailed rationale remain in those files; do not infer additional rationale. Record future consequential choices here with ID, date, status, choice, reason, consequences and references. Mark superseded entries rather than deleting them.

## UL-001 — Stable-build promotion
- **Recorded in:** [ROADMAP.md](ROADMAP.md), Development rule; [CURRENT_STATE.md](CURRENT_STATE.md), sections 1 and 6.
- **Status:** Active at the 27 September 2026 checkpoint.
- **Choice:** Implement one coherent feature at a time from the latest user-confirmed stable build. Promote only after user testing and confirmation.

## UL-002 — GitHub Pages migration
- **Recorded in:** [CURRENT_STATE.md](CURRENT_STATE.md), sections 1 and 3; [ROADMAP.md](ROADMAP.md), GitHub Pages migration.
- **Status:** Deployment confirmed in a desktop browser; Quest 2 validation outstanding at the last checkpoint.
- **Choice:** Host the exact v1.2.34 single-file application as repository-root `index.html`, without a migration refactor.

## UL-003 — Previous playtest data
- **Recorded in:** [CURRENT_STATE.md](CURRENT_STATE.md), Storage/migration decision; [ROADMAP.md](ROADMAP.md), GitHub Pages migration.
- **Status:** Active.
- **Choice:** Do not migrate old Perchance localStorage playtest data.

## UL-004 — Combat victory and house rule
- **Recorded in:** [CURRENT_STATE.md](CURRENT_STATE.md), Combat state; [ROADMAP.md](ROADMAP.md), Rulesets and house rules.
- **Status:** Active.
- **Choice:** Preserve defeated foes using `t.defeated = true`; optional `state.settings.endFightOnWeakHit` changes the End the Fight progress-roll victory result and defaults to OFF.

## UL-005 — Drum looping
- **Recorded in:** [CURRENT_STATE.md](CURRENT_STATE.md), Audio and Known failed/reverted builds.
- **Status:** Active.
- **Choice:** Use Web Audio API buffer looping; do not revert to the superseded HTML Audio overlap experiments.

## UL-006 — Optional Delphi
- **Recorded in:** [CURRENT_STATE.md](CURRENT_STATE.md), Delphi; [ROADMAP.md](ROADMAP.md), Delphi integration.
- **Status:** Active.
- **Choice:** Delphi is an optional spoken assistant. Saga remains fully playable without it.

These entries are navigation aids, not replacements for the detailed source records.
