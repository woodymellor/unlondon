# UnLondon — Knowledgebase

This file indexes durable evidence and discoveries without removing or paraphrasing the existing detailed records. The original sources remain authoritative. Add independently verified findings here as the project develops; label them **CONFIRMED**, **REPORTED**, **HYPOTHESIS** or **OPEN**.

## Existing evidence and source locations

- **CONFIRMED in the 27 September 2026 checkpoint:** The exact user-confirmed v1.2.34 baseline and migration/test record are documented in [CURRENT_STATE.md](CURRENT_STATE.md), sections 1 and 3.
- **Documented technical details:** Storage, Datasworn foundation, combat victory state and house rule, progress rendering, audio, FX, UI and Delphi integration are recorded in [CURRENT_STATE.md](CURRENT_STATE.md), section 3.
- **Documented failures and superseded experiments:** See [CURRENT_STATE.md](CURRENT_STATE.md), section 5. Do not revive abandoned approaches without a new investigation.
- **Feature designs, constraints and dependencies:** See [ROADMAP.md](ROADMAP.md). Planned functionality must not be described as implemented.
- **Live implementation:** [index.html](index.html) is the application source; inspect it before making code-level claims or changes.

## Open verification

- Quest 2 validation of the GitHub Pages deployment was still outstanding at the last recorded checkpoint (27 September 2026). Check [CURRENT_STATE.md](CURRENT_STATE.md) for a newer result before relying on this status.

No existing technical material has been moved out of or deleted from the original documents.


## Architecture and implementation knowledge migrated from the 27 September context

The following preserves context-specific detail not previously recorded in this file. The original context remains available separately as a verbatim archive.

### Source-of-truth boundaries
- **RAW:** `Ironsworn-Rulebook.pdf`, `classic.json`, `delve.json` in ChatGPT Project sources. Context notes are not game rules.
- **Implementation:** live `index.html`, the project context and the live checkpoint.
- **House rules:** explicitly identified optional Saga settings.
- **Campaign canon:** saved state and Chronicle. Use **ESTABLISHED**, **NEWLY ESTABLISHED**, **PROPOSED** and **UNKNOWN**; never silently convert the latter two into historical fact.
- **Roadmap:** proposals must remain distinguishable from implemented features.

### Roles and play
Saga handles mechanics, structured state, bookkeeping and procedural tools; WorldLens represents exterior 3D London; the player controls character choices and rolls; oracles resolve meaningful uncertainty. Delphi is an optional voice assistant for interpretation, rules, NPC portrayal, continuity and atmosphere. Delphi cannot control the player character, silently update Saga, invent established history or become a dependency. A **Rules check** interrupts storytelling to consult the actual rulebook/Datasworn sources. Follow fiction-first move handling; where multiple moves are plausible, offer possibilities rather than choosing. In dangerous combat, make the opponent's action concrete and respect initiative/control and fictional positioning. Discussed voice commands: **Start session**, **What now?**, **Rules check**, **Recap**, **Oracle**, **End session**.

### Durable data and boundaries
Separate **code** (core application), **content** (Datasworn, homebrew and distributable assets) and **campaign data** (character, Chronicle, NPCs, Threads, foes, locations and discoveries). Personal campaign data must never be baked into a public edition. The future portable/cloud campaign should include all mutable state. For procedural content generated externally, **Perchance/external tools may generate; Saga owns and saves** accepted structured campaign state. Portrait/image persistence is a separate concern and must not block saving a foe.

### Persistent interior data model
Distinguish a **location definition** (established physical topology/layout) from **campaign discovery state** (explored areas, door states, notes and changes). Both belong in campaign data. Saga owns hidden spatial structure; Delphi does not need the hidden/GM map. Generate spatial constraints rather than scripted encounters or plot.

### Foe generation and combat interpretation
Foe actions express **intent, not guaranteed outcome**. Proposed range/position changes apply only when fiction establishes them; a player-confirmed **APPLY POSITION** control is a possible future interaction, not an implemented feature. Boss combat progress may inform escalation without being treated as literal health. The Combat Progress Track owns/attaches a generated foe instance; basic combat must remain usable without generation or Delphi.

### Product and interaction lessons
Do not require the player to enter information merely to make Saga appear intelligent. Infer from existing state/actions. The manual “Now” panel was rejected because it duplicates bookkeeping; an optional pinned/active track is preferable. Quest UI should minimise typing, use compact panels, collapsible sections, controller-friendly targets and frequent actions within one or two clicks. Established visual direction: dark charcoal/iron translucent panels, warm parchment/ivory text, restrained bronze, Cinzel headings and Crimson Pro body text; cinematic effects should be subtle.

### Historical source
The user's original **Ironsworn Saga — General Project Context**, last consolidated 27 September 2026, is preserved verbatim as the separately supplied `UNLONDON_ORIGINAL_CONTEXT_2026-09-27.md`. This migration does not treat its superseded Perchance hosting paragraph as current state.
