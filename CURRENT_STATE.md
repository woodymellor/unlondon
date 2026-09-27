# Ironsworn Saga — Current State

> Authoritative quick handoff for development sessions.
>
> Last updated: 2026-09-27

## Stable baseline

**v1.2.34 — Successful End the Fight FX**

This is the latest user-confirmed stable baseline. Future work must begin here unless the user explicitly establishes a newer tested baseline.

Known artifact from the originating development session:

`ironsworn_saga_v1.2.34_successful_end_fight_fx.html`

The original sandbox path is session-local and should not be assumed to exist in future chats. Preserve/export the actual stable HTML before new implementation work.

## Hosting

Current working model:
- Saga remains a single-page HTML app used via Perchance.
- Long-term plan: migrate to GitHub Pages, but **not yet**.
- Repository **woodymellor/unlondon** currently hosts Saga-related audio and other assets.
- Do not assume the current Saga HTML itself has already been migrated into this repo.

## Storage

Implemented:
- localStorage autosave
- campaign JSON export/import
- journal text export

Not implemented:
- Google Drive/cloud backup
- `.issaga` cloud campaign files
- automatic cloud snapshots

Cloud backup is a high-priority future milestone.

## Rules/data

Embedded/integrated foundation:
- Ironsworn Classic Datasworn
- Ironsworn Delve Datasworn
- Classic assets
- Classic + Delve oracle library
- Delve moves, themes, domains and example sites
- source/page metadata and Datasworn IDs retained where implemented

Classic + Delve are treated as the default combined Ironsworn rules/content foundation.

## Main implemented campaign features

- Character sheet
- Standard action rolls
- Moves
- Vow progress
- Journey progress
- Combat progress
- Bond progress
- Oracle tools/library
- Assets/homebrew foundations
- Delve tab/tools
- Campaign State
- Session tracking
- Campaign Chronicle
- Journal
- New/reset campaign
- import/export
- dedicated Combat tab

## Combat state

Combat is a main tab.

Combat tracks support:
- progress
- End the Fight
- rename
- manual finish
- delete when appropriate

Important current victory architecture:

**Do not automatically use `finished=true` for a successful End the Fight.**

The stable approach uses:

`t.defeated = true`

This keeps the defeated foe card visible rather than causing it to disappear from active-combat rendering.

Renderer applies defeated styling for combat tracks that are finished or defeated.

### House rule

Persisted setting:

`state.settings.endFightOnWeakHit`

Default: `false`.

Approved behaviour:
- OFF → only Strong Hit on End the Fight defeats the foe.
- ON → Strong Hit or Weak Hit defeats the foe.
- Miss never defeats the foe.

This setting affects the **End the Fight progress-roll victory result**. Do not reintroduce the abandoned logic that disables the End the Fight button based on Saga's interpretation of the preceding move.

### Successful End the Fight FX

Whenever End the Fight is successful under the above rule:
- foe becomes defeated;
- completion sparks play;
- NewQuest cue plays if sound is enabled;
- existing combat hit/slash behaviour remains in its normal path.

## Progress display

- 10 progress boxes.
- 4 ticks fill one box.
- 40 ticks fill the track.
- Full box symbol is **✱**.
- At 40 ticks, the track receives a subtle completed-track glow/pulse.
- Reduced-motion preference gets a static treatment.

## Audio

Audio is hosted externally in GitHub rather than embedded in the HTML.

Repository: **woodymellor/unlondon**

Known files:
- `horn.mp3`
- `drums.mp3`
- `drums.wav`
- `drone.mp3`
- `NewQuest.mp3`
- `QuestCompleted.mp3`
- `SkillUp.mp3`
- `LevelUp.mp3`
- `slash.mp3`

### Soundboard
Implemented:
- Drums loop
- Drone loop
- Horn
- New Quest
- Quest Done
- Skill Up
- Level Up
- Stop All
- master sound ON/OFF
- persisted master volume

Switching sound OFF stops active loops/cues.

### Drum loop

The correct stable architecture is **Web Audio API buffer looping**, introduced in v1.2.18:
- fetch audio
- decode to AudioBuffer
- AudioBufferSourceNode
- `loop=true`
- `loopStart=0`
- `loopEnd=buffer.duration`
- gain node follows master volume

Do not return to the failed HTML Audio overlap/dual-deck loop experiments.

## Visual effects

Implemented/confirmed lineage includes:
- combat miss → brief red edge vignette;
- combat strong/weak hit → steel slash visual;
- combat hit → `slash.mp3` when sound is enabled;
- Oracle result → drifting runes;
- Mark Progress → warm bronze progress-box glow;
- strong Fulfill Your Vow → sparks, LevelUp audio if enabled, delayed **IRON VOW FULFILLED** ceremonial title;
- successful End the Fight → victory sparks + NewQuest cue;
- reduced-motion support.

The aesthetic target is restrained Ironlands/Nordic atmosphere, not flashy videogame UI.

## UI

- Single-page/tabbed application.
- Dark charcoal/iron translucent panels.
- Warm parchment/ivory text.
- Restrained bronze accents.
- Atmospheric landscape treatment.
- Cinzel headings/nav/branding.
- Crimson Pro body/interface.
- Dark Journal textarea.
- Compact, Quest-controller-friendly interaction.
- Avoid unnecessary typing.
- Avoid wholesale redesign of stable screens.

## Delphi

Optional ChatGPT Voice assistant named **Delphi**.

Delphi:
- helps with rules, moves, oracles, NPC portrayal, continuity and fiction;
- does not control the player's character;
- does not silently update Saga;
- is not required to play.

Current practical setup on Quest 2:
- WorldLens for exterior/3D London.
- Saga in Quest Browser for mechanics/campaign state.
- ChatGPT Voice/Delphi in Quest Browser as optional spoken assistant.

Do not design Saga features that require Delphi.

## Persistent interiors

Not implemented. Agreed roadmap direction:
- ASCII/text maps;
- persistent layouts/discovery;
- conventional pre-generated interiors;
- Delve-as-you-go maps;
- stored as campaign state;
- Delphi only needs what the player tells it.

## Foe Forge / Behaviour Engine

Not implemented. Agreed roadmap direction:
- modular constraint-aware foe/boss generation;
- archetype-driven behaviour;
- weighted **FOE ACTION**;
- FAR/NEAR/ENGAGED-style minimal situation state;
- recent-use/cooldown logic;
- progress-informed boss escalation;
- generated foe attached to a specific Combat Progress Track;
- no separate HP system;
- fully playable without Delphi.

Optional future one-click generated portrait is under investigation.

## Quest Forge / POIs

Not implemented. Agreed roadmap direction:
- persistent Points of Interest;
- constraint-aware quest archetypes/modules;
- reuse campaign POIs;
- quest information revealed progressively;
- Ironsworn/oracles determine fiction rather than a pre-written hidden script.

## NPCs / Narrative Threads

Not yet integrated as first-class Saga records. Desired eventually:
- Active / Dormant / Resolved
- weights
- search/filter
- roll NPC/thread
- durable cloud-backed storage
- Delphi briefing inclusion

## Asset work still pending

- owned Asset cards on Combat screen;
- editable owned-asset instance fields;
- Companion names/state;
- roll-aware suggestions for detectable asset triggers.

## Known failed/reverted builds

Do not use as baseline:

- **v1.3.0, v1.3.1, v1.3.2** — bulk feature experiments broke layout/sidebar; abandoned.
- **v1.2.29** — successful End the Fight set `finished=true`, causing the combat card to close/disappear.
- **v1.2.31** — `canTriggerEndFight()`/button-disable experiment broke End the Fight.
- **v1.2.12–v1.2.17 drum experiments** — overlap/native HTML Audio approaches superseded by Web Audio v1.2.18.

## Development workflow for the next agent

Before editing Saga:
1. Read this file.
2. Read `ROADMAP.md`.
3. Read the Project Source general context document if available.
4. Obtain the actual latest stable HTML; do not reconstruct it from prose.
5. Make one coherent change only.
6. Return a complete replacement HTML build when that is the requested workflow.
7. Wait for user testing before updating the stable baseline in this file.

