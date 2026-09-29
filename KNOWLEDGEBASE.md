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


## Project boundaries and reusable content packages — agreed 2026-09-29

- **Ironsworn Saga** is the generic software project. **UnLondon** is a separate setting/campaign project that may define original assets, oracles, foes, equipment, other content and limited changes to core mechanics. **Delphi** initially belongs to the setting project; separating it later is an open option.
- A proposed **Content Packages** page loads/enables multiple compatible JSON packages, not just one exclusive setting. Classic is the required base; Delve and custom packages may coexist.
- **Package vs save:** reusable JSON packages define available content and supported rule settings. Campaign saves contain mutable character state, progress, discoveries and history; campaigns using the same package remain independent.
- Distinguish original Ironsworn RAW, official expansion content, setting-specific homebrew content and explicit house rules. JSON is declarative data/configuration, not arbitrary executable JavaScript. Saga must implement any supported mechanical modification.
- Selected package identities/versions belong in campaign metadata; missing or incompatible packages require warnings. Schema, dependency resolution, conflict/override semantics and import UX are still open design questions, not established implementation.
- Future settings can supply their own JSON without duplicating or modifying Saga's core application. Reusable compatible homebrew packages may be combined across settings.


## UnLondon postcode-world model — agreed design, 2026-09-29

**Status: AGREED DESIGN / PROTOTYPE, not implemented or playtested in stable Saga.** The original standalone Locations mock-up demonstrated a postcode selector and persistent enemy/loot state; the subsequent combined Delve mock-up was exploratory. The agreed direction is to keep those responsibilities separate.

- **District (open world):** a real postcode district is a persistent area with an established population and durable state. Precise positions of all ordinary enemies need not be tracked. Rest/death may repopulate respawnable enemies without reversing permanent boss, unique-loot or discovery changes.
- **Location (named place):** a place within a district; its type may be ordinary POI, encounter, merchant, quest location, checkpoint or Delve site. A district can have any number of Delve sites, including none.
- **Delve site (expedition):** a self-contained location where official Delve site creation, exploration and objective mechanics apply. Delve progress belongs to that site, not automatically to its parent postcode district. Do not replace or silently alter official Delve mechanics with Souls-like district respawning.
- **Architectural boundary:** Classic/Delve Saga remains setting-independent; the UnLondon postcode Locations model is setting/campaign-specific. Link to generic Delve records where appropriate rather than duplicate the Delve engine in Locations.
- **Map/reference boundary:** the existing Knowledge Dashboard stays an independent browser reference. Saga does not need postcode polygons, map rendering or communication with the dashboard; a current-postcode selector is sufficient.
- **Campaign data:** distinguish reusable setting/location definitions from saved mutable district populations, individual foe status, collected loot, discovered locations and per-site Delve state. This is a design distinction, not an implemented schema.
- **Game-design analogy:** Elden Ring-style open regions containing optional self-contained dungeons; exploration of the surrounding region is independent of completing any dungeon. The analogy is a design reference, not a claim that Ironsworn or Delve supplies these open-world persistence rules.
