# PIG-Game Features Document

This document groups the 84 requirements into 8 logical features with priorities, acceptance criteria, and complexity estimates.

---

## Feature 1: Core Engine

**Description:** The foundational game engine that processes player input, manages the game loop, and maintains state consistency. This is the deterministic heart of the system that separates game logic from AI narrative generation.

### Included Requirements
- **ENG-001** - Command normalization layer for raw player input
- **ENG-002** - Convert commands into canonical action objects
- **ENG-003** - Canonical commands: move_north, move_south, move_east, move_west
- **ENG-004** - Canonical commands: look, examine, take, use, talk, attack
- **ENG-005** - Input validation after normalization
- **ENG-006** - Reject invalid/unrecognized commands gracefully
- **ENG-007** - Deterministic engine operation based on canonical actions
- **ENG-008** - Consistent, reproducible results for identical inputs
- **ENG-009** - Separation of deterministic logic from AI narrative
- **ENG-010** - Game state changes computed by engine, not AI
- **ENG-011** - Persist world state and player state
- **ENG-013** - State persistence: stats, inventory, position, tiles, NPCs, items
- **ENG-014** - State consistency between sessions
- **ENG-015** - Game loop: Read → Normalize → Validate → Execute → Persist → Generate → Output
- **ENG-016** - Game start flow with mode selection

### Acceptance Criteria
- [ ] All player inputs are normalized to canonical action objects
- [ ] Invalid commands are rejected with helpful error messages
- [ ] Game state changes are 100% deterministic and reproducible
- [ ] State can be saved and loaded with full consistency
- [ ] Game loop executes in correct sequence for every turn
- [ ] Mode selection is available at game start

### Priority: **MVP**

### Estimated Complexity: **High (5)**
- Command normalization requires robust parsing
- State persistence needs serialization/deserialization
- Determinism requires careful architecture design
- Game loop orchestrates all subsystems

---

## Feature 2: World System

**Description:** The world representation including tile-based map structure, procedural generation, directional connections, and persistence of world state.

### Included Requirements
- **WRL-001** - Tiles with unique identifiers
- **WRL-002** - Tile types (forest, dungeon, town, etc.)
- **WRL-003** - Tile descriptions
- **WRL-006** - Directional connections (north, south, east, west)
- **WRL-024** - Support directional connections
- **WRL-025** - Connections traversable via move commands
- **WRL-026** - Blocked movement when no connection exists
- **WRL-008** - Procedural world generation
- **WRL-009** - Procedurally generated worlds remain logical and consistent

### Acceptance Criteria
- [ ] World is composed of tiles with unique IDs and types
- [ ] Tiles have descriptions and directional connections
- [ ] Movement respects connections (can only move where connected)
- [ ] Procedurally generated worlds are consistent and logical
- [ ] World state persists across sessions

### Priority: **MVP**

### Estimated Complexity: **Medium-High (4)**
- Procedural generation algorithms
- Connection graph management
- World state serialization

---

## Feature 3: Entity System

**Description:** Management of all game entities including NPCs, enemies, items, and player inventory. Handles entity lifecycle, positioning, and interactions.

### Included Requirements
**NPCs:**
- **WRL-010** - NPCs with unique identifiers
- **WRL-011** - NPC names
- **WRL-012** - NPC types (friendly, neutral, hostile)
- **WRL-013** - NPC health points
- **WRL-014** - NPC armor/defense values
- **WRL-015** - NPC status effects tracking
- **WRL-016** - NPC current location (tile reference)
- **WRL-017** - NPC dialogue capabilities

**Items:**
- **WRL-018** - Items with unique identifiers
- **WRL-019** - Item names and descriptions
- **WRL-020** - Item types (weapon, armor, consumable, quest)
- **WRL-021** - Items collectible by player
- **WRL-022** - Item effects when used
- **WRL-023** - Items exist in inventory or world tiles
- **WRL-004** - Tiles track NPCs present
- **WRL-005** - Tiles track items present

**Player Inventory:**
- **PLR-006** - Player inventory for items
- **PLR-007** - Add items to inventory (take command)
- **PLR-008** - Remove items from inventory (use/drop)
- **PLR-009** - Examine items in inventory
- **PLR-010** - Inventory capacity limits

### Acceptance Criteria
- [ ] NPCs have stats (HP, armor) and can occupy tiles
- [ ] Items have types, can be collected and used
- [ ] Inventory system supports add/remove/examine operations
- [ ] Entities track their location in the world
- [ ] Status effects can be applied to entities

### Priority: **MVP**

### Estimated Complexity: **Medium (3)**
- Entity data models
- Inventory management
- Location tracking

---

## Feature 4: Combat System

**Description:** Deterministic combat mechanics including damage calculation, status effects, and combat flow. The AI narrates but never modifies combat outcomes.

### Included Requirements
- **CBT-001** - Deterministic combat system
- **CBT-002** - Damage calculation considers attacker stats and defender armor
- **CBT-003** - System computes all numeric combat results
- **CBT-004** - AI does NOT modify health, damage, or numeric values
- **CBT-005** - AI describes combat outcomes narratively only
- **CBT-006** - Status effects on entities
- **CBT-007** - Status effects affect combat calculations deterministically
- **CBT-008** - Status effects have duration and effect type
- **CBT-009** - AI describes status effects without modifying mechanics
- **CBT-010** - AI describes combat actions, reactions, outcomes
- **CBT-011** - AI adds flavor/narrative to combat encounters
- **CBT-012** - AI does NOT decide combat results or override engine

### Acceptance Criteria
- [ ] Combat damage is calculated deterministically based on stats
- [ ] Status effects modify combat calculations correctly
- [ ] AI provides narrative descriptions but cannot alter outcomes
- [ ] Combat results are reproducible for identical inputs
- [ ] Status effects have proper duration tracking

### Priority: **MVP**

### Estimated Complexity: **Medium (3)**
- Damage formulas
- Status effect system
- AI boundary enforcement

---

## Feature 5: Story System

**Description:** Quest and narrative management including story nodes, triggers, dependencies, and progression tracking. Enables both scripted and emergent storytelling.

### Included Requirements
- **STY-001** - Story nodes for quests, events, narrative arcs
- **STY-002** - Story nodes attachable to tiles, NPCs, items
- **STY-003** - Story nodes with unique identifiers
- **STY-004** - Story node types: quest, event, arc
- **STY-005** - Story triggers based on player actions
- **STY-006** - Story triggers based on game state changes
- **STY-007** - Story triggers based on location entry
- **STY-008** - Triggers activate story nodes when conditions met
- **STY-009** - Story nodes support dependencies on other nodes
- **STY-010** - System checks dependencies before activating nodes
- **STY-011** - Story progression is deterministic
- **STY-012** - Story Mode as game start option
- **STY-013** - Story Mode provides narrative-driven gameplay
- **STY-014** - Story Mode may combine with procedural generation
- **WRL-007** - Tiles may have story hooks attached

### Acceptance Criteria
- [ ] Story nodes can be attached to world elements (tiles, NPCs, items)
- [ ] Triggers activate based on actions, state changes, or location entry
- [ ] Dependencies prevent premature story progression
- [ ] Story Mode option available at game start
- [ ] Progression is deterministic and reproducible

### Priority: **MVP**

### Estimated Complexity: **High (5)**
- Trigger system design
- Dependency resolution
- Story state management

---

## Feature 6: AI Narrative Layer

**Description:** AI-powered narrative generation that describes the world, writes dialogue, and adds flavor while strictly adhering to a read-only contract with game state.

### Included Requirements
- **AI-001** - AI generates narrative descriptions of the world
- **AI-002** - AI writes dialogue for NPCs
- **AI-003** - AI adds flavor text to game events
- **AI-004** - AI suggests story hooks and narrative opportunities
- **AI-005** - AI generates player-facing responses after engine processing
- **AI-006** - AI does NOT modify player or NPC stats
- **AI-007** - AI does NOT modify player inventory
- **AI-008** - AI does NOT move the player character
- **AI-009** - AI does NOT spawn or remove entities
- **AI-010** - AI does NOT resolve quests or mark story nodes complete
- **AI-011** - AI operates in read-only capacity regarding game state
- **AI-012** - System enforces AI boundaries at architecture level
- **AI-013** - No meta-commands exposed to AI
- **AI-014** - AI has no access to admin/debug commands

### Acceptance Criteria
- [ ] AI generates descriptions, dialogue, and flavor text
- [ ] AI operates strictly read-only on game state
- [ ] Architecture enforces AI boundaries (cannot modify state)
- [ ] No meta-commands or debug access available to AI
- [ ] AI responses enhance player experience without affecting gameplay

### Priority: **MVP**

### Estimated Complexity: **Medium-High (4)**
- AI integration architecture
- Prompt engineering
- Boundary enforcement mechanisms

---

## Feature 7: Player System

**Description:** Player character management including creation, stats, progression, and core player actions available in the game.

### Included Requirements
**Character Creation:**
- **PLR-001** - Character creation at game start
- **PLR-002** - Random character generation
- **PLR-003** - Custom character creation
- **PLR-004** - Character creation defines initial stats
- **PLR-005** - Character creation defines starting inventory

**Player Stats:**
- **PLR-011** - Player health points
- **PLR-012** - Player mana points
- **PLR-013** - Player stats affecting gameplay
- **PLR-014** - Stats affect deterministic calculations
- **PLR-015** - Player current position in world

**Player Actions:**
- **PLR-016** - Move between connected tiles
- **PLR-017** - Look at current surroundings
- **PLR-018** - Examine specific objects/NPCs
- **PLR-019** - Take items from environment
- **PLR-020** - Use items from inventory
- **PLR-021** - Talk to NPCs
- **PLR-022** - Attack enemies

### Acceptance Criteria
- [ ] Character creation supports random and custom options
- [ ] Player has HP, MP, and stats affecting gameplay
- [ ] All core actions (move, look, examine, take, use, talk, attack) work
- [ ] Player position is tracked in the world
- [ ] Stats affect deterministic calculations appropriately

### Priority: **MVP**

### Estimated Complexity: **Medium (3)**
- Character creation flow
- Stat system design
- Action handlers

---

## Feature 8: Game Modes & Setup

**Description:** Game mode configuration including random world generation, story-driven campaigns, and setup flow with difficulty and rule customization.

### Included Requirements
- **ENG-016** - Game start flow with mode selection
- **ENG-017** - Difficulty settings: Easy, Normal, Hard
- **ENG-018** - Configurable rules: Permadeath, Magic scarcity, Technology level
- **ENG-012** - Save/load functionality
- **STY-012** - Story Mode as game start option
- **STY-013** - Story Mode provides narrative-driven gameplay
- **STY-014** - Story Mode may combine with procedural generation
- **WRL-008** - Procedural world generation
- **WRL-009** - Procedurally generated worlds remain logical

### Acceptance Criteria
- [ ] Mode selection available at game start (Random World, Story Mode)
- [ ] Difficulty settings affect gameplay parameters
- [ ] Configurable rules (Permadeath, Magic, Technology) are applied
- [ ] Save/load functionality works across sessions
- [ ] Story Mode can combine with procedural elements

### Priority: **v1.1** (Save/load could be MVP, full config is v1.1)

### Estimated Complexity: **Medium (3)**
- Setup flow UI/logic
- Configuration management
- Save/load system

---

## Summary

| Feature | Priority | Complexity | Req Count | Key Risk Areas |
|---------|----------|------------|-----------|----------------|
| Core Engine | MVP | High (5) | 15 | Determinism, State persistence |
| World System | MVP | Med-High (4) | 9 | Procedural generation |
| Entity System | MVP | Medium (3) | 16 | Entity lifecycle |
| Combat System | MVP | Medium (3) | 12 | AI boundaries |
| Story System | MVP | High (5) | 14 | Trigger complexity |
| AI Narrative | MVP | Med-High (4) | 14 | Boundary enforcement |
| Player System | MVP | Medium (3) | 12 | Character creation flow |
| Game Modes | v1.1 | Medium (3) | 9 | Configuration system |

### MVP Requirements: 77 (92%)
### v1.1 Requirements: 5 (6%)
### v2.0 Requirements: 2 (2%)

**Total: 84 requirements**

---

## Dependency Graph

```
Core Engine
├── World System
│   ├── Entity System
│   └── Story System
├── Combat System
│   └── Entity System
├── Player System
│   └── Entity System (Inventory)
├── AI Narrative Layer
│   ├── World System
│   ├── Entity System
│   ├── Combat System
│   └── Story System
└── Game Modes & Setup
    ├── World System
    ├── Story System
    └── Player System
```

**Critical Path:** Core Engine → World System → Entity System → Player System
