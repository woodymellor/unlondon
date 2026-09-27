# Ironsworn Saga — Current State / Session Checkpoint

> **Purpose:** finest-grain development handoff. This file should let a new ChatGPT session resume work if the previous chat ends abruptly.
>
> Read in this order when resuming: **Project Context → ROADMAP.md → this file**.
>
> Update this file **during development**, not only after a feature is finished.
>
> Last updated: 2026-09-27

## 1. Live session checkpoint

### Stable baseline

**v1.2.34 — Successful End the Fight FX**

This is the latest **user-confirmed stable build**.

Known artifact name from the originating session:

`ironsworn_saga_v1.2.34_successful_end_fight_fx.html`

The old sandbox path is session-local and must not be assumed to exist in a future chat. Before implementing code, obtain the actual stable HTML rather than reconstructing Saga from documentation.

### Current working build

**None.**

No code change is currently in progress beyond v1.2.34. No untested successor build should be assumed to exist.

### What we are working on right now

The immediate work has been **project continuity infrastructure**, specifically protecting Saga development against ChatGPT conversation-length/session loss.

The continuity hierarchy has now been explicitly defined as:

1. **General Project Context** — durable accumulated knowledge, design philosophy, architecture, lessons learned and major feature concepts. Stored as a ChatGPT Project Source.
2. **ROADMAP.md** — strategic/living plan: intended features, priorities, dependencies and deferred ideas. Stored in this GitHub repository.
3. **CURRENT_STATE.md** — this file. Finest-grain live development checkpoint: exactly what the current/last session was doing, how far it got, what was tested, unresolved problems, current files/builds and the precise next action.

### Work completed in this session

- Created a consolidated **Ironsworn Saga General Project Context** Markdown document for upload to ChatGPT Project Sources.
- Created `ROADMAP.md` in `woodymellor/unlondon`.
- Created the first version of `CURRENT_STATE.md` in `woodymellor/unlondon`.
- Clarified that the original Current State document was too much like a static technical snapshot.
- Redefined Current State as a **live session checkpoint/workbench**.
- This revision implements that distinction while retaining the stable technical facts needed for safe continuation.

### Testing/status

No Saga application code was changed in this continuity-documentation session, so there is no new Saga build to test.

**Stable application remains v1.2.34.**

### Unresolved / decisions still open

No implementation bug is currently being debugged.

Major roadmap priorities remain open, including:
- GitHub Pages migration;
- Google Drive/cloud backup;
- NPCs/Narrative Threads;
- persistent POIs/Locations;
- Foe Forge + Behaviour Engine;
- Quest Forge;
- Combat Asset improvements;
- optional generated foe portraits.

See `ROADMAP.md` for strategic detail.

### Precise next action

When development resumes:

1. User chooses the next feature to implement.
2. Read the Project Context, then `ROADMAP.md`, then this checkpoint.
3. Obtain the actual **v1.2.34 stable HTML** (or a newer user-confirmed stable build if this file has subsequently been updated).
4. Record the chosen feature below as **Current task** and record the source artifact under **Current working build** before/when modification begins.
5. Implement **one coherent feature only**.
6. Update this checkpoint as meaningful progress/debugging decisions occur.
7. User tests the produced build in Perchance/Quest.
8. Only after user confirmation promote it to **Stable baseline**.

---

## 2. How to maintain this checkpoint

During an active coding session, the top section should contain enough detail to resume without the previous conversation.

At minimum keep these fields current:

- **Stable baseline** — last user-tested and confirmed build.
- **Current working build** — exact filename/version being modified or tested.
- **Current task** — one coherent feature currently being implemented.
- **Last completed step** — what was just changed.
- **Current test result** — what the user tested and what happened.
- **Known issue / hypothesis** — exact failure and likely cause if debugging.
- **Relevant implementation details** — functions/state keys/selectors/files that matter to the active task.
- **Next action** — the single most useful next step.
- **Do not repeat** — failed approaches discovered during this session.

Example of the intended granularity:

```text
Stable baseline: v1.2.34
Current working build: v1.2.35-test-2
Current task: Owned Asset cards in Combat
Last completed step: Combat card rendering works.
Test result: Quest rendering passed; Companion name does not persist after reload.
Relevant state: state.ownedAssets[...].instanceFields
Next action: inspect save/normalisation path for owned asset instance fields.
Do not repeat: storing Companion name only on transient rendered Datasworn definition.
```

When a feature is successfully tested:
- promote that build to Stable baseline;
- move durable architectural lessons to the Project Context when warranted;
- update `ROADMAP.md` completion/status;
- clear/reset the active working-build/task/debug fields for the next feature.

---

## 3. Stable technical state — v1.2.34

The remainder of this file records technical facts needed to avoid regressions while resuming work.

### Hosting

- Saga remains a single-page HTML app used via Perchance.
- Long-term plan is GitHub Pages, but **not yet**.
- Repository `woodymellor/unlondon` currently hosts Saga-related audio and continuity documents.
- Do not assume the stable Saga HTML itself is already stored in the repo.

### Storage

Implemented:
- localStorage autosave
- campaign JSON export/import
- journal text export

Not implemented:
- Google Drive/cloud backup
- `.issaga` cloud campaign files
- automatic cloud snapshots

Cloud backup is a high-priority roadmap milestone.

### Rules/data foundation

- Ironsworn Classic Datasworn
- Ironsworn Delve Datasworn
- Classic assets
- Classic + Delve oracle library
- Delve moves, themes, domains and example sites
- Datasworn IDs/source metadata retained where implemented

Classic + Delve are treated as the default combined Ironsworn foundation.

### Main implemented campaign features

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

### Combat state

Combat is a main tab.

Combat tracks support progress, End the Fight, rename, manual finish and deletion where appropriate.

**Critical victory architecture: do not automatically use `finished=true` for successful End the Fight.**

Stable approach:

`t.defeated = true`

This keeps the defeated foe card visible. The renderer applies defeated styling to combat tracks that are finished or defeated.

#### House rule

Persisted setting:

`state.settings.endFightOnWeakHit`

Default: `false`.

Approved behaviour:
- OFF → only Strong Hit on End the Fight defeats the foe.
- ON → Strong Hit or Weak Hit defeats the foe.
- Miss never defeats the foe.

This changes the **End the Fight progress-roll victory result**. Do not restore the abandoned logic that disabled the End the Fight button based on Saga's interpretation of preceding-move eligibility.

#### Successful End the Fight FX

On every successful End the Fight under the above rule:
- foe becomes defeated;
- completion sparks play;
- NewQuest cue plays if sound is enabled;
- normal combat hit/slash behaviour remains in its existing path.

### Progress display

- 10 progress boxes.
- 4 ticks per full box.
- 40 ticks fills the track.
- Full box symbol: **✱**.
- At 40 ticks, subtle completed-track glow/pulse.
- Reduced-motion preference receives a static treatment.

### Audio

Hosted externally in `woodymellor/unlondon`:
- `horn.mp3`
- `drums.mp3`
- `drums.wav`
- `drone.mp3`
- `NewQuest.mp3`
- `QuestCompleted.mp3`
- `SkillUp.mp3`
- `LevelUp.mp3`
- `slash.mp3`

Soundboard includes Drums, Drone, Horn, New Quest, Quest Done, Skill Up, Level Up, Stop All, master sound ON/OFF and persisted master volume. Turning sound off stops active loops/cues.

#### Drum loop

Correct stable architecture is **Web Audio API buffer looping**, introduced in v1.2.18:
- fetch audio;
- decode AudioBuffer;
- AudioBufferSourceNode;
- `loop=true`;
- `loopStart=0`;
- `loopEnd=buffer.duration`;
- gain node follows master volume.

Do not return to failed HTML Audio overlap/dual-deck loop experiments.

### Visual effects

Confirmed lineage includes:
- combat miss → brief red edge vignette;
- combat Strong/Weak Hit → steel slash visual;
- combat hit → `slash.mp3` when sound enabled;
- Oracle → drifting runes;
- Mark Progress → warm bronze progress glow;
- strong Fulfill Your Vow → sparks + LevelUp if enabled + delayed **IRON VOW FULFILLED** title;
- successful End the Fight → victory sparks + NewQuest cue;
- reduced-motion support.

Aesthetic target: restrained Ironlands/Nordic atmosphere, not flashy videogame UI.

### UI

- single-page/tabbed app;
- dark charcoal/iron translucent panels;
- warm parchment/ivory text;
- restrained bronze accents;
- Cinzel headings/nav/branding;
- Crimson Pro body/interface;
- dark Journal textarea;
- compact Quest-controller-friendly interaction;
- minimise typing;
- avoid wholesale redesign of stable screens.

### Delphi

Optional ChatGPT Voice assistant named **Delphi**.

Current Quest setup:
- WorldLens → exterior/3D London;
- Saga → mechanics/campaign state;
- ChatGPT Voice/Delphi → optional spoken assistant.

Delphi helps with rules, moves, oracles, NPC portrayal, continuity and fiction. It does not control the player's character or silently update Saga.

**Saga must remain fully playable without Delphi.**

---

## 4. Roadmap features not yet implemented

These summaries exist only to prevent a future agent from mistaking planned features for current functionality. Full design belongs in `ROADMAP.md` and the Project Context.

### Persistent Interiors
Not implemented. Planned: ASCII maps, persistent layout/discovery, conventional generated interiors plus Delve-as-you-go, stored in campaign state.

### Foe Forge / Behaviour Engine
Not implemented. Planned: modular constraint-aware foe/boss generation, archetypes, weighted FOE ACTION, minimal FAR/NEAR/ENGAGED state, cooldown/repetition logic, progress-informed escalation and attachment to a specific Combat Progress Track. No separate HP system. Must work without Delphi.

### Quest Forge / POIs
Not implemented. Planned: persistent Points of Interest and constraint-aware quest structures that reveal progressively and defer actual fiction to Ironsworn/oracles.

### NPCs / Narrative Threads
Not first-class Saga records yet. Planned durable status/weight/search/roll functionality and Delphi briefing inclusion.

### Combat Asset improvements
Pending: owned Asset cards in Combat, editable asset-instance fields/Companion state and roll-aware suggestions for mechanically detectable asset triggers.

### Generated foe portraits
Not implemented. One-click portrait concept remains exploratory. Hybrid Perchance/GitHub architecture requires proof-of-concept testing and an image-persistence solution.

---

## 5. Known failed/reverted builds

Do not use these as baseline:

- **v1.3.0 / v1.3.1 / v1.3.2** — bulk feature experiments broke layout/sidebar; abandoned.
- **v1.2.29** — successful End the Fight used `finished=true`, causing combat card to close/disappear.
- **v1.2.31** — `canTriggerEndFight()` / button-disable experiment broke End the Fight.
- **v1.2.12–v1.2.17 drum experiments** — HTML Audio overlap/native approaches superseded by Web Audio v1.2.18.

## 6. Handoff rule

If a future chat finds this file mid-debugging, **continue from the live checkpoint at the top rather than restarting the feature from the roadmap**.

Do not promote a working/test build to stable merely because code was generated. Stable means the user has tested and confirmed it.
