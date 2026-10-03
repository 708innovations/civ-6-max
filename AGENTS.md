# AGENTS.md - Developer & AI Agent Guidelines for Civilization VI: Max Mod

This repository contains the source code, art assets, documentation, and ModBuddy project files for **Max - Civilization VI Mod**, a custom expansion mod introducing leader **Max** and the **Soupmeister** civilization.

All AI agents and developers operating in this repository must adhere to the architecture, coding conventions, asset standards, and guardrails outlined below.

---

## 1. Mod Overview & Thematic Architecture

The mod revolves around an eccentric, culinary, and heist-driven economic engine documented in [`README.md`](README.md):

- **Leader:** `LEADER_MAX` (Max)
  - **Leader Ability:** `TRAIT_LEADER_KLEPTOMANIA` — City Centers start with +5 Product Slots; Seaports and Stock Exchanges add +3 slots each; tiered Amenity bonuses for collecting silverware sets (**Loaded**, **Fully Loaded**, **Overloaded**).
  - **Unique Action:** `ACTION_POCKET_SILVERWARE` — Executed by Naked Homeless Men in foreign districts to pillage 1 district level and steal Fork (+2 Culture), Spoon (+2 Science), or Plate (+1 Culture, +1 Science) products without consuming charges.
- **Civilization:** `CIVILIZATION_SOUPMEISTER`
  - **Civilization Ability:** `TRAIT_CIVILIZATION_SOUPMEISTER` — Unlocks the **Make Egg Drop Soup** (`PROJECT_MAKE_EGG_DROP_SOUP`) project granting +1 Population, +1 Amenity, and 6-tile radius +10% Food. Permanently stacks +1 Food to the host city's Granary (up to +3), unlocking a 50% project production discount at the cap.
- **Unique District:** `DISTRICT_THE_DYLAN` (replaces Neighborhood) — Grants +200 Housing, -2 Amenities, and spawns 3 Barbarian Tanks upon completion.
- **Unique Units:**
  - `UNIT_NAKED_HOMELESS_MAN` — Scaling immortal melee infiltrator (matches highest infantry stats), +1 capacity per era, respawns with 1 HP at nearest Soup Kitchen/Capital, deals 5 passive damage to adjacent units within 1 tile, throws silverware for +20 Ranged Strength (-40 Bombard), has 2 charges causing 100 Grievances and -1 tile Appeal in foreign City Centers.
  - `UNIT_NUCLEAR_SATELLITE` — Replaces Observation Balloon; support air unit, Astronomy unlock, 10 Gold maintenance, Sight of 9 unobscured by terrain, grants +1 Range to adjacent bombard units.
- **Unique Improvements:**
  - `IMPROVEMENT_SOUP_KITCHEN` — Unlocks at Craftsmanship; +30% Production & +50 EXP for Naked Homeless Men; acts as resurrection anchor; boosts Egg Drop Soup radius Food to +20%.
  - `IMPROVEMENT_SHITBUCKS_COFFEE` — Unlocks at Capitalism; units spending 10 Gold gain +2 Movement for 10 turns; +1 Amenity if city owns an improved Coffee resource.

---

## 2. Directory Structure & Key Files

```
c:\Code\civ-6-max\
├── AGENTS.md                                # This developer and agent rulebook
├── README.md                                # Complete mod gameplay and lore documentation
├── docs\
│   └── images\                              # 2D/3D art asset specifications and source images
│       ├── atlas-civ-icon.md                # Civ icon atlas specification
│       ├── atlas-leader-icon.md             # Leader icon atlas specification
│       ├── atlas-uu-icon.md                 # Unit icon atlas specification
│       ├── diplomacy-background.md          # 1920x1080 diplomacy room background spec
│       ├── diplomacy-static-model.md        # 2D fallback leader documentation & specs
│       ├── diplomacy-static-model.png       # Transparent 2048x2048 fallback leader model
│       ├── diplomacy-static-model-generated.jpg # Raw generated leader source image
│       ├── dom-background.md                # Dawn of Man & loading screen background specs
│       ├── dom-background.jpg               # Full-color 1920x1080 DOM speech background
│       ├── dom-background-loading.jpg       # Muted dark-green 1920x1080 loading screen wash
│       ├── dom-leader-portrait.md           # 1024x1024 transparent DOM leader cutout spec
│       └── leader-selection-portrait.md     # 2048x2048 transparent setup/loading portrait spec
└── MaxLeader\                               # Civilization VI ModBuddy SDK Project
    ├── MaxLeader.civ6proj                   # Main ModBuddy project configuration
    ├── MaxLeader.civ6sln                    # Visual Studio solution file
    ├── MaxLeader.Art.xml                    # Project art dependencies and libraries
    ├── ArtDefs\                             # Art definition files mapping game elements to BLPs
    │   └── FallbackLeaders.artdef           # Maps LEADER_MAX to FALLBACK_NEUTRAL_MAX
    ├── Textures\                            # Texture source files (.dds) and Firaxis metadata (.tex)
    │   ├── FALLBACK_NEUTRAL_MAX.dds         # DirectDraw Surface texture (DXT5 / BC3)
    │   └── FALLBACK_NEUTRAL_MAX.tex         # TextureInstance metadata XML
    └── XLPs\                                # Package definitions compiled into .blp files
        ├── LeaderFallbacks.xlp              # 2D fallback leader textures
        └── UILeaders.xlp                    # UI portraits, loading screens, and icons
```

---

## 3. Database & Coding Conventions

### A. Database Implementation: Pure XML

- All game database definitions (Civilizations, Leaders, Traits, Modifiers, Units, Districts, Improvements, Projects) are written in **pure XML** following official Firaxis schemas.
- XML tags must use strict naming prefixes:
  - Leaders: `LEADER_MAX`
  - Civilizations: `CIVILIZATION_SOUPMEISTER`
  - Traits: `TRAIT_LEADER_...`, `TRAIT_CIVILIZATION_...`
  - Modifiers: `MODIFIER_MAX_...`
  - Dynamic Modifiers: `MODIFIERTYPE_MAX_...`
  - Types: `TYPE_...`
- **Localization Keys:** All text keys must follow standard conventions (`LOC_LEADER_MAX_NAME`, `LOC_TRAIT_KLEPTOMANIA_DESCRIPTION`, etc.) with English localized text placed in `Text_Max.xml` under `<LocalizedText>` tables.

### B. Dynamic Gameplay Mechanics: Lua Scripting

- Complex mechanics not achievable through XML `<Modifiers>` alone (e.g. Pocket Silverware district pillage + product award logic, Naked Homeless Man passive 5 aura damage, Shitbucks 10-Gold movement purchase, respawn at nearest Soup Kitchen) must be implemented via **Lua scripts** using Civ VI Gameplay Events (`Events` / `GameEvents`).
- Place Lua scripts in `MaxLeader/Scripts/` and register them in `MaxLeader.civ6proj` under `<InGameActions>` -> `<AddGameplayScripts>`.

---

## 4. Art Asset Pipeline & Technical Specifications

All art assets created or edited must conform strictly to the resolutions, formats, and compression schemes specified in [`docs/images/`](docs/images/):

| Asset Type                       | Target File                  | Resolution                  | Format / Compression                | Transparency               | Documentation                                                              |
| :------------------------------- | :--------------------------- | :-------------------------- | :---------------------------------- | :------------------------- | :------------------------------------------------------------------------- |
| **Diplomacy Static Model**       | `FALLBACK_NEUTRAL_MAX.dds`   | `2048 x 2048`               | `BC3 / DXT5` or `PF_R8G8B8A8_UNORM` | 32-bit RGBA (Alpha cutout) | [`diplomacy-static-model.md`](docs/images/diplomacy-static-model.md)       |
| **Dawn of Man Background**       | `DOM_BACKGROUND_MAX.dds`     | `1920 x 1080`               | `BC1 / DXT1` or `PF_B8G8R8A8_UNORM` | 24-bit RGB (No alpha)      | [`dom-background.md`](docs/images/dom-background.md)                       |
| **Loading Screen Wash**          | `LOADING_BACKGROUND_MAX.dds` | `1920 x 1080`               | `BC1 / DXT1` (Muted dark green)     | 24-bit RGB (No alpha)      | [`dom-background.md`](docs/images/dom-background.md)                       |
| **DOM Leader Portrait**          | `DOM_LEADER_MAX.dds`         | `1024 x 1024`               | `BC3 / DXT5`                        | 32-bit RGBA (Alpha cutout) | [`dom-leader-portrait.md`](docs/images/dom-leader-portrait.md)             |
| **Leader Selection Portrait**    | `PORTRAIT_LEADER_MAX.dds`    | `2048 x 2048`               | `BC3 / DXT5`                        | 32-bit RGBA (Alpha cutout) | [`leader-selection-portrait.md`](docs/images/leader-selection-portrait.md) |
| **Icon Atlases (Civ/Leader/UU)** | `ICON_ATLAS_MAX_*.dds`       | Various (256, 80, 50, etc.) | `BC3 / DXT5`                        | 32-bit RGBA                | [`atlas-leader-icon.md`](docs/images/atlas-leader-icon.md)                 |

### Asset Integration Chain:

1. Source PNG/JPG saved in `docs/images/`.
2. DDS texture generated with full mipmaps in `MaxLeader/Textures/`.
3. Firaxis metadata XML created in `MaxLeader/Textures/<NAME>.tex`.
4. Registered in package list `MaxLeader/XLPs/<CLASS>.xlp`.
5. Wired into ArtDef (`FallbackLeaders.artdef`, `Civilizations.artdef`, `Leaders.artdef`).
6. Declared in `MaxLeader.civ6proj`.

---

## 5. Agent Operational Guardrails & Rules

When modifying or adding files in this codebase, all AI agents must follow these operational rules:

1. **Preserve Documentation Integrity:**
   - Never delete or overwrite established lore, trait mechanics, or design rationales in [`README.md`](README.md) or [`docs/images/`](docs/images/).
   - Update corresponding markdown documentation whenever an art asset or XML structure is updated.
2. **Strict XML Validation:**
   - All XML files must be well-formed with matching closing tags, correct casing, and valid attributes.
   - Every text key referenced in `<GameData>` must have an entry in `<LocalizedText>` for English (`Language="en_US"`).
3. **Prevent Committing Temporary Binary Build Artifacts:**
   - Never track or commit ModBuddy user files (`.suo`), compilation logs (`.log`), or compiler cache directories (`bin/`, `obj/`).
   - Keep `.gitignore` strictly enforced.
4. **Maintain Clickable Markdown Links:**
   - Always reference repository files using markdown file links with forward slashes (e.g. [`README.md`](README.md) or [`docs/images/dom-background.md`](docs/images/dom-background.md)).
5. **Enforce Prettier on Markdown Files:**
   - All Markdown documentation (`*.md`) must be formatted using Prettier (`npx prettier --write <file>`).
   - Run Prettier on any Markdown file created or updated before committing changes.
6. **Verify Changes Locally:**
   - Validate file existence, syntax, and image dimensions via shell or Python commands before presenting changes to the user.

---

## 6. Git Commit Standards

All commits in this repository must follow a standardized structure adhering to Conventional Commits, a bulleted body, and explicit provenance trailers.

### Commit Format Template

```gitcommit
<type>(<optional-scope>): <subject line in present imperative>

- <Bullet point detailing specific change>
- <Bullet point detailing rationale or technical context>
- <Bullet point noting updated documentation or assets>

Signed-off-by: <Name> <<email>>
Assisted-by: <tool>/<model>
Conversation: <uuid>
```

### Commit Rules:

1. **Conventional Commits:**
   - Allowed types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`.
   - Keep subject lines concise (<= 72 characters), lowercase after the colon, with no trailing period.
2. **Bulleted Body:**
   - The body must be separated from the subject by a blank line.
   - Every line in the body must be a bullet point starting with `- `.
3. **Mandatory Trailers:**
   - Must include three trailers at the very end:
     - `Signed-off-by: <Name> <<email>>` — Committer name and email.
     - `Assisted-by: <tool>/<model>` — Tool and model identifier (e.g. `agy/gemini-3.8-flash`).
     - `Conversation: <uuid>` — Active agent conversation UUID (e.g. `e08e28a0-240b-4888-ba02-351e6592d028`).
