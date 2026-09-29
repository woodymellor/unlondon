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


## Additional established decisions from the original project context

### UL-007 — Rules and canon authority
- **Status:** Active.
- **Choice:** The supplied rulebook and Datasworn sources govern RAW; implementation, house rules, campaign canon and roadmap proposals are separate categories. Campaign ideas marked PROPOSED or UNKNOWN are not established history.
- **Reason:** Avoid invented mechanics and fabricated campaign continuity.

### UL-008 — Structure without scripted story
- **Status:** Active.
- **Choice:** Saga generates useful structure, spatial constraints and pressure; Ironsworn/oracles establish the actual fiction. Do not pre-write quests or require Delphi as a hidden GM.
- **Reason:** Preserve solo Ironsworn's play-to-find-out approach.

### UL-009 — Minimise duplicated bookkeeping
- **Status:** Active.
- **Choice:** Reject the manually maintained “Now” panel; infer current information from existing state where possible. A pinned/active track may be considered.
- **Reason:** Do not require the player to enter information merely so Saga appears intelligent.

### UL-010 — Persistent interiors
- **Status:** Agreed design; implementation planned.
- **Choice:** Use lightweight persistent ASCII/text maps, not a full graphical dungeon engine. Keep established location topology and campaign discovery state separate; Delphi does not need hidden map data.
- **Reason:** Provide repeatable interior exploration without excessive complexity or duplicating WorldLens.

### UL-011 — Procedural foe and combat boundaries
- **Status:** Agreed design; implementation planned.
- **Choice:** Constraint-aware modular foes attach to Combat Progress Tracks; weighted FOE ACTION describes intent, not automatic outcomes. Use minimal positional state and no separate boss HP.
- **Reason:** Preserve Ironsworn mechanics, fiction-first resolution and low bookkeeping.

### UL-012 — Generation and persistence ownership
- **Status:** Active architectural decision for future features.
- **Choice:** External services such as Perchance may generate; Saga owns and persists accepted structured state. Portrait persistence is separate from foe-data persistence.
- **Reason:** Campaign continuity must not depend on a transient generator.

### UL-013 — One codebase for editions
- **Status:** Active future architecture.
- **Choice:** Use one core codebase with configuration/content differences for personal and potential public editions. Separate code, content and campaign data.
- **Reason:** Avoid divergent implementations and exposure of personal campaign state.

### UL-014 — Project Factory migration
- **Date:** 29 September 2026.
- **Status:** Active.
- **Choice:** Keep the original context verbatim in a separate archive; use a shorter context as entry point and distribute durable details into GitHub documents. Existing roadmap, checkpoint and application source are preserved.
- **Reason:** Improve fresh-chat continuity without losing prior decisions or technical detail.


## UL-014 — Separate tool and setting projects
- **Date:** 2026-09-29
- **Status:** Agreed; organisational split to be carried out separately.
- **Choice:** Ironsworn Saga is the generic web-tool project; UnLondon is a separate setting/campaign project owning its worldbuilding, homebrew content and setting-specific house rules. Delphi initially lives with UnLondon; a third project remains optional.
- **Reason:** Separate software development from creative setting/campaign work without making Saga dependent on one setting.
- **Consequences:** Saga owns generic implementation and repository; UnLondon owns its setting-specific material.

## UL-015 — JSON content packages
- **Date:** 2026-09-29
- **Status:** Agreed architecture; not implemented.
- **Choice:** Plan a Content Packages page to import/select/enable multiple compatible JSON packages. Classic is required; Delve and custom setting/reusable homebrew packages can coexist. Future settings load their own JSON rather than fork Saga.
- **Reason:** Reuse the same tool across settings and share compatible custom content.
- **Consequences:** Design package IDs/versions, validation, dependencies and collision handling. Persist package selection with each campaign and warn about missing requirements.

## UL-016 — Content, rules and campaign-state separation
- **Date:** 2026-09-29
- **Status:** Agreed architectural boundary; implementation planned.
- **Choice:** Keep official RAW, homebrew content and explicit house-rule modifications distinct. JSON supplies declarative content/configuration; Saga implements supported mechanical changes without executing arbitrary imported code. Package definitions remain separate from mutable campaign saves, so multiple campaigns can independently use the same package.
- **Reason:** Preserve rules provenance, security, portability and campaign independence.
- **Consequences:** UnLondon rules must not silently become Saga defaults; schema and supported rule-modification capabilities require subsequent design.


## UL-017 — Postcode districts are open-world areas, not Delve sites
- **Date:** 2026-09-29
- **Status:** Agreed design; not implemented in stable Saga.
- **Choice:** Treat London postcode districts as persistent open-world regions with saved enemy populations, NPCs, loot, discoveries and checkpoints. Ordinary enemies may respawn on rest/death; unique boss defeats and unique loot collection persist. Do not require precise enemy positions or give each district a compulsory Delve progress track.
- **Reason:** Support free exploration and Souls/Elden Ring-style persistence without forcing a whole postcode district into a single dungeon expedition.
- **Consequences:** Add named locations within districts; a district may have zero or several self-contained dungeons. Exact gameplay rules remain to be playtested.

## UL-018 — Delve sites remain optional, self-contained locations
- **Date:** 2026-09-29
- **Status:** Agreed design; not implemented in stable Saga.
- **Choice:** Use existing Delve mechanics for appropriate individual locations inside open-world districts. Keep generic Classic + Delve Saga setting-independent; do not merge Delve's site progress or exploration rules into every postcode district.
- **Reason:** Preserve the distinction between open-world exploration and structured site expeditions, and avoid reinventing or duplicating Delve.
- **Consequences:** Return to the original Locations prototype as the conceptual foundation and add named places with optional Delve-site links. The combined Locations + Delve prototype is exploratory, not the intended integrated architecture.

## UL-019 — Existing Knowledge Dashboard remains an external map
- **Date:** 2026-09-29
- **Status:** Agreed for the experimental UnLondon workflow.
- **Choice:** Use the existing Knowledge Dashboard in a separate browser window; do not reproduce it or integrate it with Saga. Select the current postcode district manually in Saga.
- **Reason:** Reuse the working map and avoid unnecessary duplication and integration work.
- **Consequences:** The London Locations system requires persistent district state and a postcode selector, not a map engine or imported geographic boundaries.
