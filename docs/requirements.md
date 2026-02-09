# PIG-Game Requirements Document

This document contains the extracted requirements from the PIG-Game design document, organized by category with priorities and references.

---

## Engine Requirements

### Command Normalization

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| ENG-001 | The system SHALL implement a command normalization layer that processes raw player input | Must | High-Level System Architecture |
| ENG-002 | The system SHALL convert all player commands into canonical action objects | Must | Command Normalization Pipeline |
| ENG-003 | The system SHALL support canonical commands: move_north, move_south, move_east, move_west | Must | Command Normalization Pipeline |
| ENG-004 | The system SHALL support canonical commands: look, examine, take, use, talk, attack | Must | Command Normalization Pipeline |
| ENG-005 | The system SHALL handle input validation after normalization | Must | Main Game Loop |
| ENG-006 | The system SHALL reject invalid or unrecognized commands gracefully | Must | Main Game Loop |

### Deterministic Logic

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| ENG-007 | The game engine SHALL operate deterministically based on canonical action objects | Must | Core Design Principles |
| ENG-008 | The engine SHALL produce consistent, reproducible results for identical inputs | Must | Core Design Principles |
| ENG-009 | The system SHALL separate deterministic game logic from AI narrative generation | Must | Core Design Principles |
| ENG-010 | All game state changes SHALL be computed by the engine, not the AI | Must | Core Design Principles |

### State Persistence

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| ENG-011 | The system SHALL persist world state and player state | Must | High-Level System Architecture |
| ENG-012 | The system SHALL support save/load functionality | Should | World/State Persistence |
| ENG-013 | State persistence SHALL capture: player stats, inventory, position, world tiles, NPCs, items | Must | World Model |
| ENG-014 | The system SHALL maintain state consistency between game sessions | Must | World/State Persistence |

### Game Loop

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| ENG-015 | The main game loop SHALL follow: Read input → Normalize → Validate → Execute → Persist → Generate narrative → Output | Must | Main Game Loop |
| ENG-016 | The system SHALL support game start flow with mode selection | Must | Game Start Flow |
| ENG-017 | The system SHALL support difficulty settings: Easy, Normal, Hard | Should | Game Start Flow |
| ENG-018 | The system SHALL support configurable rules: Permadeath, Magic scarcity, Technology level | Could | Game Start Flow |

---

## World Requirements

### Tile System

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| WRL-001 | The world SHALL be composed of tiles with unique identifiers | Must | World Model |
| WRL-002 | Each tile SHALL have a type (e.g., forest, dungeon, town) | Must | World Model |
| WRL-003 | Each tile SHALL have a description | Must | World Model |
| WRL-004 | Each tile SHALL track NPCs present at that location | Must | World Model |
| WRL-005 | Each tile SHALL track items present at that location | Must | World Model |
| WRL-006 | Each tile SHALL define connections to adjacent tiles (north, south, east, west) | Must | World Model |
| WRL-007 | Each tile MAY have story hooks attached | Should | World Model |
| WRL-008 | The system SHALL support procedural world generation | Should | Core Design Principles |
| WRL-009 | Procedurally generated worlds SHALL remain logical and consistent | Must | Core Design Principles |

### NPC System

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| WRL-010 | NPCs SHALL have unique identifiers | Must | World Model |
| WRL-011 | NPCs SHALL have a name | Must | World Model |
| WRL-012 | NPCs SHALL have a type (friendly, neutral, hostile) | Must | World Model |
| WRL-013 | NPCs SHALL have health points | Must | World Model |
| WRL-014 | NPCs SHALL have armor/defense values | Must | World Model |
| WRL-015 | NPCs SHALL track status effects | Must | World Model |
| WRL-016 | NPCs SHALL have a current location (tile reference) | Must | World Model |
| WRL-017 | NPCs MAY have dialogue and conversation capabilities | Should | World Model |

### Item System

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| WRL-018 | Items SHALL have unique identifiers | Must | World Model |
| WRL-019 | Items SHALL have a name and description | Must | World Model |
| WRL-020 | Items SHALL have a type (weapon, armor, consumable, quest item, etc.) | Must | World Model |
| WRL-021 | Items SHALL be collectible by the player | Must | World Model |
| WRL-022 | Items MAY have effects when used | Should | World Model |
| WRL-023 | Items SHALL exist in either player inventory or world tiles | Must | World Model |

### Connections

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| WRL-024 | Tiles SHALL support directional connections: north, south, east, west | Must | World Model |
| WRL-025 | Connections SHALL be traversable via move commands | Must | Command Normalization Pipeline |
| WRL-026 | Movement SHALL be blocked if no connection exists in the requested direction | Must | Main Game Loop |

---

## Combat Requirements

### Damage Calculation

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| CBT-001 | The combat system SHALL be deterministic | Must | Deterministic Combat System |
| CBT-002 | Damage calculation SHALL consider attacker stats and defender armor | Must | Deterministic Combat System |
| CBT-003 | The system SHALL compute all numeric combat results | Must | Deterministic Combat System |
| CBT-004 | The AI SHALL NOT modify health, damage, or any numeric values during combat | Must | AI Usage Contract |
| CBT-005 | The AI SHALL describe combat outcomes narratively only | Must | Deterministic Combat System |

### Status Effects

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| CBT-006 | The system SHALL support status effects on entities | Must | World Model |
| CBT-007 | Status effects SHALL affect combat calculations deterministically | Must | Deterministic Combat System |
| CBT-008 | Status effects SHALL have duration and effect type | Should | World Model |
| CBT-009 | The AI SHALL describe status effects narratively without modifying their mechanics | Must | AI Usage Contract |

### Combat AI

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| CBT-010 | The AI SHALL describe combat actions, reactions, and outcomes | Must | Deterministic Combat System |
| CBT-011 | The AI SHALL add flavor and narrative to combat encounters | Should | Deterministic Combat System |
| CBT-012 | The AI SHALL NOT decide combat results or override engine calculations | Must | AI Usage Contract |

---

## Story Requirements

### Story Nodes

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| STY-001 | The system SHALL support story nodes for quests, events, and narrative arcs | Must | Story System |
| STY-002 | Story nodes SHALL be attachable to tiles, NPCs, and items | Must | Story System |
| STY-003 | Story nodes SHALL have unique identifiers | Must | Story System |
| STY-004 | Story nodes SHALL have a type: quest, event, or arc | Must | Story System |

### Triggers

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| STY-005 | The system SHALL support story triggers based on player actions | Must | Story System |
| STY-006 | The system SHALL support story triggers based on game state changes | Must | Story System |
| STY-007 | The system SHALL support story triggers based on location entry | Must | Story System |
| STY-008 | Triggers SHALL activate story nodes when conditions are met | Must | Story System |

### Dependencies

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| STY-009 | Story nodes SHALL support dependencies on other story nodes | Should | Story System |
| STY-010 | The system SHALL check dependencies before activating story nodes | Should | Story System |
| STY-011 | Story progression SHALL be deterministic based on player actions and triggers | Must | Story System |

### Story Mode

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| STY-012 | The system SHALL support Story Mode as a game start option | Must | Game Start Flow |
| STY-013 | Story Mode SHALL provide narrative-driven gameplay | Should | Game Start Flow |
| STY-014 | Story Mode MAY combine with procedural world generation | Could | Game Start Flow, Core Design Principles |

---

## AI Requirements

### Narrative Layer

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| AI-001 | The AI SHALL generate narrative descriptions of the world | Must | AI Usage Contract |
| AI-002 | The AI SHALL write dialogue for NPCs | Must | AI Usage Contract |
| AI-003 | The AI SHALL add flavor text to game events | Should | AI Usage Contract |
| AI-004 | The AI SHALL suggest story hooks and narrative opportunities | Could | AI Usage Contract |
| AI-005 | The AI SHALL generate player-facing responses after engine processing | Must | High-Level System Architecture |

### Usage Contract

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| AI-006 | The AI SHALL NOT modify player or NPC stats | Must | AI Usage Contract |
| AI-007 | The AI SHALL NOT modify player inventory | Must | AI Usage Contract |
| AI-008 | The AI SHALL NOT move the player character | Must | AI Usage Contract |
| AI-009 | The AI SHALL NOT spawn or remove entities (NPCs, items) | Must | AI Usage Contract |
| AI-010 | The AI SHALL NOT resolve quests or mark story nodes complete | Must | AI Usage Contract |
| AI-011 | The AI SHALL operate in a read-only capacity regarding game state | Must | AI Usage Contract |
| AI-012 | The system SHALL enforce AI boundaries at the architecture level | Must | High-Level System Architecture |

### No Meta Commands

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| AI-013 | The system SHALL NOT expose meta-commands to the AI | Must | Core Design Principles |
| AI-014 | The AI SHALL NOT have access to administrative or debug commands | Must | Core Design Principles |

---

## Player Requirements

### Character Creation

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| PLR-001 | The system SHALL support character creation at game start | Must | Game Start Flow |
| PLR-002 | The system SHALL support random character generation | Should | Game Start Flow |
| PLR-003 | The system SHALL support custom character creation | Should | Game Start Flow |
| PLR-004 | Character creation SHALL define initial player stats | Must | World Model |
| PLR-005 | Character creation SHALL define starting inventory | Should | World Model |

### Inventory

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| PLR-006 | The player SHALL have an inventory to store collected items | Must | World Model |
| PLR-007 | The system SHALL support adding items to inventory (take command) | Must | Command Normalization Pipeline |
| PLR-008 | The system SHALL support removing items from inventory (use/drop) | Should | Command Normalization Pipeline |
| PLR-009 | The system SHALL support examining items in inventory | Should | Command Normalization Pipeline |
| PLR-010 | Inventory SHALL have capacity limits | Could | World Model |

### Stats

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| PLR-011 | The player SHALL have health points | Must | World Model |
| PLR-012 | The player SHALL have mana points | Must | World Model |
| PLR-013 | The player SHALL have stats affecting gameplay | Must | World Model |
| PLR-014 | Stats SHALL affect deterministic calculations (combat, skill checks) | Must | Deterministic Combat System |
| PLR-015 | The player SHALL have a current position in the world | Must | World Model |

### Player Actions

| ID | Requirement | Priority | Reference |
|----|-------------|----------|-----------|
| PLR-016 | The player SHALL be able to move between connected tiles | Must | Command Normalization Pipeline |
| PLR-017 | The player SHALL be able to look at their current surroundings | Must | Command Normalization Pipeline |
| PLR-018 | The player SHALL be able to examine specific objects/NPCs | Must | Command Normalization Pipeline |
| PLR-019 | The player SHALL be able to take items from the environment | Must | Command Normalization Pipeline |
| PLR-020 | The player SHALL be able to use items from inventory | Must | Command Normalization Pipeline |
| PLR-021 | The player SHALL be able to talk to NPCs | Must | Command Normalization Pipeline |
| PLR-022 | The player SHALL be able to attack enemies | Must | Command Normalization Pipeline |

---

## Requirements Summary

| Category | Must | Should | Could | Total |
|----------|------|--------|-------|-------|
| Engine | 10 | 3 | 1 | 14 |
| World | 14 | 3 | 2 | 19 |
| Combat | 7 | 2 | 0 | 9 |
| Story | 7 | 3 | 1 | 11 |
| AI | 8 | 2 | 1 | 11 |
| Player | 9 | 9 | 2 | 20 |
| **Total** | **55** | **22** | **7** | **84** |

---

*Document generated from PIG-game-design.md*
