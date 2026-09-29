# Ironsworn Saga — Roadmap

> Living roadmap for implementation continuity. Update this file when priorities, scope, or completion status change.
>
> Last consolidated: 2026-09-27

## Development rule

Implement **one coherent feature at a time** from the latest user-confirmed stable build. A feature becomes baseline only after the user has tested and confirmed it. Do not use abandoned higher-numbered experiments as a starting point.

## Current foundation

- [x] Ironsworn Classic + Delve Datasworn integration
- [x] Character sheet and action rolls
- [x] Vow, Journey, Combat and Bond progress tracks
- [x] Dedicated Combat tab
- [x] Oracle Library
- [x] Delve tools
- [x] Assets and homebrew foundations
- [x] Campaign State, Chronicle and Journal
- [x] localStorage autosave
- [x] JSON campaign import/export
- [x] GitHub-hosted sound assets
- [x] Web Audio drum loop
- [x] Contextual visual/audio effects
- [x] ✱ full progress-box symbol and completed-track glow
- [x] Persistent defeated-foe visual state
- [x] House rule: End the Fight can succeed on Weak Hit
- [x] Victory FX on every successful End the Fight

**Confirmed stable baseline: v1.2.34**

## Priority infrastructure

### GitHub Pages migration
Status: deployed; desktop/browser launch confirmed 2026-09-27. Quest 2 validation remains.

- [x] Exact confirmed stable v1.2.34 moved to repository-root `index.html` with no functional refactor.
- [x] GitHub Pages enabled from `main` / root.
- [x] Live deployment opened successfully at `https://woodymellor.github.io/unlondon/`.
- [x] Existing Perchance localStorage deliberately not migrated; it contained playtest data only.
- [ ] Validate the GitHub Pages build in Quest 2.
- [ ] After Quest validation, treat GitHub Pages as the development baseline.
- Only after migration is fully validated consider splitting HTML/CSS/JS/data into separate files.

### Cloud backup
Status: high priority.

Preferred target: Google Drive.

- Keep localStorage for immediate autosave.
- Add optional Google authentication and Drive sync.
- Prefer narrow permissions such as `drive.file` where practical.
- Save a user-visible portable campaign file, potentially `.issaga` with JSON internally.
- Include all mutable campaign state.
- Debounce cloud sync after local saves.
- Show unobtrusive sync status.
- Keep session/snapshot generations rather than relying only on one overwritten file.
- End Session is a natural snapshot boundary.
- Provide reliable restore/load.
- Never embed secret credentials in client HTML/JavaScript.

Cloud durability should precede systems whose value depends heavily on long-term persistence.

## Campaign-world data

### NPCs and Narrative Threads
Status: planned.

- Durable campaign records, not cache-only data.
- Active / Dormant / Resolved status.
- Notes/descriptions.
- Optional weights.
- Search/filter.
- Weighted ROLL NPC / ROLL THREAD.
- Portable export.
- Include active entries in Delphi briefing.

### Points of Interest
Status: planned; foundational for Quest Forge.

A POI may eventually hold/connect:
- name and type/tags
- world/location reference
- persistent interior
- associated NPCs
- Narrative Threads
- quests/vows
- foes
- history/session visits
- notes

## Persistent Interiors / Locations
Status: agreed roadmap feature.

Goal: lightweight persistent spatial exploration for interiors WorldLens cannot represent.

### Core
- ASCII/text-based maps.
- Tiny data structures.
- Persistent layout.
- Persistent fog-of-war/discovery state.
- Return later to exactly the same layout.
- Hidden → discovered → explored states.
- Quest-friendly reveal/navigation controls.
- Save inside campaign/cloud state.
- Delphi does not need a hidden GM map.

### Mode A — conventional interior
Generate coherent hidden topology up front. Templates may include house, pub, office, warehouse, church, station, hospital, sewer/tunnel, ruin and dungeon. Aim for plausible connectivity, not architectural simulation.

### Mode B — Delve as you go
Begin with the entrance/current area. Existing Delve mechanics/oracles establish new areas and connections. Add them to the ASCII map as discovered; once established, topology becomes campaign canon. Reuse existing Datasworn themes/domains/site tools.

**Boundary:** generate space, not scripted encounters or plot.

## Foe Forge
Status: agreed roadmap feature.

Goal: distinctive modular foes and Elden-Ring-style bosses while retaining Ironsworn mechanics.

### Foe profile
Potential output:
- name/title
- Ironsworn rank
- appearance/presence
- instinct/desire
- primary and optional secondary archetype
- signature behaviours
- tells
- vulnerabilities
- reactions
- arena/environment interactions
- complications
- optional escalation/phases

### Constraint-based modular generation
Candidate archetypes:
- Bruiser
- Skirmisher
- Ambusher
- Artillery
- Controller
- Swarm
- Hunter
- Defender
- specialist/caster packages as justified

Modules need compatibility metadata such as `requires`, `supports`, `themes`, and `incompatible`. Deliberate compatible hybrids are allowed; nonsense combinations are excluded.

### Foe Behaviour Engine
- Add **FOE ACTION** to attached generated foes.
- Weighted actions; common behaviours are more likely.
- Context changes weights.
- Recent-use penalties/cooldowns reduce repetition.
- Simple range model such as FAR / NEAR / ENGAGED.
- Minimise manual state entry.
- Foe action states intent, not guaranteed outcome.
- Suggested position changes can be accepted after fiction establishes them.
- No tactical grid/facing/movement-point system.

### Boss phases
- No HP system.
- Combat progress may make escalation available without claiming progress literally equals health.
- Thresholds can vary.
- Phase transitions should be accepted when fiction warrants.
- Phases modify behaviours/weights.

### Combat-track integration
Architectural requirement: a generated foe instance attaches to a specific Combat Progress Track.

Possible combat creation choices:
- Basic Combat
- Generate Foe
- Generate Boss
- Attach Saved Foe

Basic combat must remain simple and fully usable.

## Generated foe portraits
Status: optional; investigate.

Desired UX: one-click **CREATE PORTRAIT**, automatically prompted from the generated foe description. No normal prompt-engineering UI.

Possible architectures:
- Perchance AI while hosted on Perchance.
- External image service on GitHub Pages.
- Hybrid Perchance Foe Forge embedded in GitHub-hosted Saga.

Before adopting the hybrid, test on Quest 2:
1. Perchance inside GitHub-hosted iframe.
2. AI image generation inside that iframe.
3. Cross-origin `postMessage` back to Saga.

Determine durable image persistence before relying on portraits.

## Quest Forge / POI Quest Generator
Status: agreed roadmap concept.

Goal: modular quests built around campaign POIs, with constraint-aware generation and discovery rather than pre-written adventures.

Candidate archetypes:
- Find
- Recover
- Rescue
- Investigate
- Hunt
- Deliver/Escort
- Protect
- Sabotage/Destroy
- Escape

Design:
- archetype defines structural grammar;
- choose compatible POIs using tags;
- preferentially reuse established campaign POIs;
- allow new POIs when needed;
- reveal only currently established quest information;
- keep later stages/open slots hidden and flexible;
- let Ironsworn/oracles establish actual fiction;
- generated structure must tolerate discoveries that change assumptions.

Long-term loop:

**Explore → POIs → quests → NPCs/foes → threads → future quests → location history**

## Delphi integration
Status: planned optional enhancement.

- Export/copy compact Delphi Campaign Briefing.
- Include character/resources, active tracks, Campaign State, recent Chronicle, owned assets and active NPCs/threads.
- End Session can help prepare the updated briefing.
- Potential Open ChatGPT/Project convenience link.
- Saga must remain fully playable without Delphi.

Do not prioritise deep realtime API/voice integration while Quest Browser + ChatGPT Voice works well.

## Combat assets
Status: planned.

- Show owned Asset cards at bottom of Combat.
- Consider preferentially surfacing combat-relevant assets while retaining access to all.
- Separate immutable Datasworn asset definitions from user-owned asset instances.
- Editable instance state, especially Companion names/selections/condition.
- Suggest mechanically detectable asset triggers after rolls.
- Suggestions only; never silently apply effects.

## Rulesets and house rules
Status: future architecture.

Separate official content sources from house rules.

- Classic + Delve default.
- Potential optional Starforged and Sundered Isles Datasworn packages later.
- Homebrew should ideally become a content package/source.
- Current implemented house rule: **End the Fight succeeds on Weak Hit**, default OFF.

Do not reinterpret that rule as merely changing preceding-move eligibility; the approved behaviour changes the End the Fight progress-roll victory result.

## Public edition
Status: future.

Maintain one core codebase with configuration/content differences rather than two divergent implementations.

- Personal edition = user's workflow, experimental features, homebrew and integrations.
- Public edition = clean defaults, no personal campaign data, redistribution/licensing reviewed, generic setup.
- Personal edition can be the playtest/bleeding-edge channel; public edition receives tested features.

## Explicitly deferred/rejected for now

- Manual “Now” panel requiring duplicate fictional bookkeeping.
- Deep embedded ChatGPT/API voice integration.
- Tactical-grid combat.
- Separate HP system for bosses.
- Full graphical dungeon engine when ASCII is sufficient.
- Giving Delphi hidden interior/GM map data by default.


## Supplementary specifications retained from original context (29 September 2026 migration)

These refine existing planned features; they do **not** change implementation status.

- **Delphi briefing:** Fresh voice chats may use Project sources and established campaign records. A compact export should support character/resources, active tracks, Campaign State, recent Chronicle, assets and active NPCs/Threads. Useful discussed voice commands: Start session, What now?, Rules check, Recap, Oracle, End session.
- **Persistent interiors:** Preserve both the permanent location definition and the separate campaign discovery state (door states, explored areas, notes and changes). Saga owns hidden spatial data; Delphi only needs what play reveals.
- **Foe behaviour:** If position changes are suggested, apply them only after fiction establishes the change. An explicit player-confirmed APPLY POSITION interaction is a possible design, not a committed implementation.
- **Quest fog-of-war:** Templates may retain unresolved slots, e.g. a clue leading to a compatible `[industrial]` or `[river]` POI selected only when that stage is reached. Prefer existing compatible POIs while permitting new ones.
- **Portrait hybrid:** For any external generation path, prove Quest 2 iframe generation and cross-origin `postMessage`; accepted foe data must persist in Saga even if portrait storage is unresolved.
- **Public edition:** Separate code, content and campaign data; do not embed personal campaign data in the public application.


## Setting-independent content packages
Status: agreed architecture; not implemented. Added 2026-09-29.

- Saga is the reusable, setting-independent application; UnLondon is a separate setting/campaign project. Future settings use their own JSON packages without forking Saga.
- Provide a **Content Packages** page to import, list, enable and disable JSON packages. Classic remains the required foundation; Delve and compatible custom packages may be enabled together.
- Distinguish **official content**, **custom setting content** (assets, oracles, creatures, equipment, etc.) and **house rules** that modify core mechanics. Keep official RAW unchanged; mechanical overrides require explicit, supported application behaviour, not executable JavaScript in JSON.
- Packages may declare identifiers, versions and dependencies. Validate compatibility and warn about missing required packages; avoid silent content collisions.
- Persist the selected package IDs/versions with each campaign and restore that selection when loading; warn rather than silently substituting missing content.
- **Package ≠ campaign save:** packages define reusable content and supported rules/configuration; saves hold characters, progress, discoveries, Chronicle and other mutable campaign state. Multiple campaigns can use the same package independently.
- Support multiple compatible packages simultaneously, including reusable homebrew across settings. Exact JSON schema, merge/override policy and UI details remain to be designed.
- Keep UnLondon-specific JSON and worldbuilding in the separate UnLondon project; Saga owns the generic importer, validation, package management and supported rules mechanisms.
- Delphi initially belongs with UnLondon as its setting-aware voice assistant; reconsider a separate Delphi project if it becomes reusable across settings.
