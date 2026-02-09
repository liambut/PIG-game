# PIG-Game User Stories

This document breaks down the 8 PIG-Game features into implementable user stories.

---

## Core Engine (FEAT-001)

### STORY-001: Basic Command Parsing
**As a** player, **I want** to type natural language commands **so that** the game understands my intentions without memorizing exact syntax.

**Acceptance Criteria:**
- Given I type "go north", "move north", "walk north", or "n"
- When the command is processed
- Then it normalizes to canonical action `move_north`

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-001

---

### STORY-002: Complex Command Parsing
**As a** player, **I want** to use multi-word commands with targets **so that** I can interact with specific objects and NPCs.

**Acceptance Criteria:**
- Given I type "take the rusty sword", "pick up sword", or "get sword"
- When the command is processed
- Then it normalizes to canonical action `take` with target `rusty_sword`

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-001

---

### STORY-003: Command Validation
**As a** player, **I want** to receive helpful feedback when I type invalid commands **so that** I can learn the game controls quickly.

**Acceptance Criteria:**
- Given I type an unrecognized command
- When the system cannot normalize it
- Then I receive a helpful message suggesting valid commands

**Story Points:** 2  
**Priority:** P2  
**Related Feature:** FEAT-001

---

### STORY-004: Game Loop Initialization
**As a** player, **I want** the game to start and display my current location **so that** I know where I am and can begin playing.

**Acceptance Criteria:**
- Given the game starts successfully
- When the main loop begins
- Then I see my current tile description and available exits

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-001

---

### STORY-005: Input Processing Loop
**As a** player, **I want** the game to continuously accept and process my commands **so that** I can play without interruptions.

**Acceptance Criteria:**
- Given the game is running
- When I enter a command and press return
- Then the game processes it and presents the result within 1 second

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-001

---

### STORY-006: Action Execution
**As a** player, **I want** my commands to affect the game world **so that** my actions have meaningful consequences.

**Acceptance Criteria:**
- Given I enter a valid canonical action
- When the action is executed
- Then the game state updates appropriately and the change is reflected

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-001

---

### STORY-007: State Persistence (Save)
**As a** player, **I want** to save my progress **so that** I can resume my adventure later.

**Acceptance Criteria:**
- Given I type "save" or "save game"
- When the command executes
- Then a save file is created with all current game state

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-001

---

### STORY-008: State Persistence (Load)
**As a** player, **I want** to load a previous save **so that** I can continue from where I left off.

**Acceptance Criteria:**
- Given I have a valid save file
- When I type "load" or select it from the menu
- Then the game restores to the exact saved state

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-001

---

## World System (FEAT-002)

### STORY-009: Tile Definition
**As a** developer, **I want** to define tiles with type, description, and properties **so that** the world has distinct locations.

**Acceptance Criteria:**
- Given a tile configuration
- When the tile is created
- Then it has: id, type, description, connections, npcs[], items[]

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-002

---

### STORY-010: Tile Registry
**As a** developer, **I want** a registry to store and retrieve tiles **so that** I can manage the world efficiently.

**Acceptance Criteria:**
- Given multiple tiles exist
- When I request a tile by ID
- Then the correct tile object is returned instantly

**Story Points:** 2  
**Priority:** P1  
**Related Feature:** FEAT-002

---

### STORY-011: Directional Connections
**As a** player, **I want** locations to connect in cardinal directions **so that** I can navigate the world intuitively.

**Acceptance Criteria:**
- Given I'm at a tile with a north connection
- When I move north
- Then I arrive at the connected tile and see its description

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-002

---

### STORY-012: Bidirectional Linking
**As a** developer, **I want** tile connections to be bidirectional by default **so that** I don't manually link both directions.

**Acceptance Criteria:**
- Given I connect Tile A north to Tile B
- When I check Tile B's connections
- Then Tile B has a south connection back to Tile A

**Story Points:** 2  
**Priority:** P2  
**Related Feature:** FEAT-002

---

### STORY-013: Movement Validation
**As a** player, **I want** to be blocked from moving through non-existent connections **so that** the world feels coherent.

**Acceptance Criteria:**
- Given I'm at a tile with no west exit
- When I try to move west
- Then I receive a message that I cannot go that way

**Story Points:** 2  
**Priority:** P1  
**Related Feature:** FEAT-002

---

### STORY-014: Look Command
**As a** player, **I want** to re-examine my current location **so that** I can refresh my memory of the surroundings.

**Acceptance Criteria:**
- Given I'm in any location
- When I type "look" or "l"
- Then I see the full location description again

**Story Points:** 1  
**Priority:** P2  
**Related Feature:** FEAT-002

---

### STORY-015: Procedural World Generation
**As a** player, **I want** each new game to have a unique world layout **so that** replayability is high.

**Acceptance Criteria:**
- Given I start a new Random World game
- When the world generates
- Then it creates 20+ connected tiles with logical geography

**Story Points:** 8  
**Priority:** P2  
**Related Feature:** FEAT-002

---

### STORY-016: World Coherence
**As a** player, **I want** generated worlds to make geographic sense **so that** immersion isn't broken.

**Acceptance Criteria:**
- Given a procedurally generated world
- When I examine tile transitions
- Then ocean doesn't connect directly to desert without transition zones

**Story Points:** 5  
**Priority:** P3  
**Related Feature:** FEAT-002

---

## Entity System (FEAT-003)

### STORY-017: NPC Definition
**As a** developer, **I want** to define NPCs with stats and behavior types **so that** the world feels populated.

**Acceptance Criteria:**
- Given an NPC configuration
- When the NPC is created
- Then it has: id, name, type, health, armor, location, dialogue

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-018: NPC Spawning
**As a** developer, **I want** NPCs to spawn at designated locations **so that** the world starts populated.

**Acceptance Criteria:**
- Given world generation completes
- When tiles are finalized
- Then NPCs are placed at their designated tile locations

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-019: Item Definition
**As a** developer, **I want** to define items with properties and effects **so that** players can find useful objects.

**Acceptance Criteria:**
- Given an item configuration
- When the item is created
- Then it has: id, name, type, description, weight, value, effects[]

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-020: Item Placement
**As a** player, **I want** to find items in the world **so that** I can discover loot and equipment.

**Acceptance Criteria:**
- Given I enter a tile with items
- When I look around
- Then I see a list of items present in the location

**Story Points:** 2  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-021: Player Inventory
**As a** player, **I want** an inventory to store collected items **so that** I can carry equipment and loot.

**Acceptance Criteria:**
- Given I have items
- When I type "inventory" or "i"
- Then I see a list of all items I'm carrying

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-022: Taking Items
**As a** player, **I want** to pick up items from my current location **so that** I can collect useful objects.

**Acceptance Criteria:**
- Given an item exists in my current tile
- When I type "take [item]"
- Then the item moves to my inventory and disappears from the tile

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-003

---

### STORY-023: Dropping Items
**As a** player, **I want** to drop items from my inventory **so that** I can manage my carrying capacity.

**Acceptance Criteria:**
- Given I have an item in my inventory
- When I type "drop [item]"
- Then the item leaves my inventory and appears in the current tile

**Story Points:** 2  
**Priority:** P2  
**Related Feature:** FEAT-003

---

### STORY-024: Examine Command
**As a** player, **I want** to examine items and NPCs closely **so that** I can learn more about them.

**Acceptance Criteria:**
- Given an item or NPC is present
- When I type "examine [target]"
- Then I see a detailed description of the target

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-003

---

## Combat System (FEAT-004)

### STORY-025: Combat Initiation
**As a** player, **I want** to attack enemies **so that** I can engage in combat.

**Acceptance Criteria:**
- Given an enemy is in my current location
- When I type "attack [enemy]"
- Then combat mode begins with turn order determined

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-004

---

### STORY-026: Combat Targeting
**As a** player, **I want** to specify which enemy to attack **so that** I can focus fire in multi-enemy encounters.

**Acceptance Criteria:**
- Given multiple enemies are present
- When I type "attack goblin" 
- Then my attacks target specifically the goblin, not other enemies

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-004

---

### STORY-027: Turn-Based Combat
**As a** player, **I want** combat to proceed in turns **so that** tactics and strategy matter.

**Acceptance Criteria:**
- Given combat has started
- When it's my turn
- Then I can choose an action; enemies act on their turns

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-004

---

### STORY-028: Damage Calculation
**As a** player, **I want** damage to be calculated from my stats and equipment **so that** character building matters.

**Acceptance Criteria:**
- Given I have 15 strength and a sword
- When I attack an enemy with 5 armor
- Then damage = (base + strength modifier) - armor reduction

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-004

---

### STORY-029: Critical Hits
**As a** player, **I want** a chance to deal critical damage **so that** combat has exciting moments.

**Acceptance Criteria:**
- Given I make an attack roll
- When the roll exceeds the critical threshold
- Then damage is multiplied by the critical multiplier

**Story Points:** 3  
**Priority:** P3  
**Related Feature:** FEAT-004

---

### STORY-030: Status Effect Application
**As a** player, **I want** attacks to apply status effects **so that** combat has depth and variety.

**Acceptance Criteria:**
- Given I hit with a poisoned weapon
- When damage is dealt
- Then the enemy gains "poisoned" status taking damage over time

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-004

---

### STORY-031: Status Effect Duration
**As a** player, **I want** status effects to expire after their duration **so that** combat remains balanced.

**Acceptance Criteria:**
- Given an enemy has a 3-turn poison effect
- When 3 turns pass
- Then the poison effect is removed automatically

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-004

---

### STORY-032: Combat Resolution
**As a** player, **I want** combat to end when all enemies are defeated **so that** I know when I'm safe.

**Acceptance Criteria:**
- Given I defeat the last enemy
- When their health reaches 0
- Then combat ends, XP is awarded, and loot becomes available

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-004

---

## Story System (FEAT-005)

### STORY-033: Story Node Definition
**As a** developer, **I want** to define narrative nodes **so that** story content can be attached to world elements.

**Acceptance Criteria:**
- Given a story node configuration
- When created
- Then it has: id, trigger, conditions, text, next_nodes[]

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-034: Story Node Attachment
**As a** developer, **I want** to attach story nodes to tiles, NPCs, and items **so that** narrative is woven into the world.

**Acceptance Criteria:**
- Given a story node exists
- When attached to a tile
- Then the node triggers when the tile's conditions are met

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-035: Entry Triggers
**As a** player, **I want** story events to trigger when I enter locations **so that** the world feels reactive.

**Acceptance Criteria:**
- Given a tile has an entry trigger story node
- When I move to that tile
- Then the story event fires and displays narrative text

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-036: Interaction Triggers
**As a** player, **I want** story events to trigger when I interact with NPCs/items **so that** conversations feel meaningful.

**Acceptance Criteria:**
- Given an NPC has an interaction trigger
- When I talk to them
- Then the story event fires and may advance quest state

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-037: Quest Definition
**As a** developer, **I want** to define quests with objectives **so that** players have goals.

**Acceptance Criteria:**
- Given a quest configuration
- When created
- Then it has: id, name, description, objectives[], rewards[]

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-038: Quest Progress Tracking
**As a** player, **I want** to see my active quest progress **so that** I know what to do next.

**Acceptance Criteria:**
- Given I have active quests
- When I type "quests" or "journal"
- Then I see all active quests with completed and remaining objectives

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-005

---

### STORY-039: Story Hook Generation
**As a** player, **I want** locations to have story hooks **so that** I'm drawn into the narrative.

**Acceptance Criteria:**
- Given I enter a location
- When I look around
- Then I see hints at possible storylines or mysteries

**Story Points:** 3  
**Priority:** P3  
**Related Feature:** FEAT-005

---

## AI Narrative Layer (FEAT-006)

### STORY-040: Location Description Generation
**As a** player, **I want** AI-generated location descriptions **so that** every place feels unique and vivid.

**Acceptance Criteria:**
- Given I enter a tile or type "look"
- When the description is generated
- Then I see rich, atmospheric prose describing the location

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-006

---

### STORY-041: Item Description Generation
**As a** player, **I want** AI-generated item descriptions **so that** items feel special and detailed.

**Acceptance Criteria:**
- Given I examine an item
- When the description is generated
- Then I see a vivid description that fits the item's type and world context

**Story Points:** 3  
**Priority:** P3  
**Related Feature:** FEAT-006

---

### STORY-042: NPC Dialogue Generation
**As a** player, **I want** NPCs to respond with AI-generated dialogue **so that** conversations feel natural.

**Acceptance Criteria:**
- Given I talk to an NPC
- When the dialogue is generated
- Then I see contextually appropriate speech matching the NPC's personality

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-006

---

### STORY-043: Dialogue Memory
**As a** player, **I want** NPCs to remember our previous conversations **so that** dialogue feels continuous.

**Acceptance Criteria:**
- Given I've spoken to an NPC before
- When I talk to them again
- Then their responses reference or acknowledge prior interactions

**Story Points:** 5  
**Priority:** P3  
**Related Feature:** FEAT-006

---

### STORY-044: State Modification Prevention
**As an** admin, **I want** the AI blocked from modifying game state **so that** determinism is preserved.

**Acceptance Criteria:**
- Given the AI generates a response
- When it's processed
- Then any attempts to modify stats/inventory/position are stripped out

**Story Points:** 5  
**Priority:** P1  
**Related Feature:** FEAT-006

---

### STORY-045: Prompt Guardrails
**As an** admin, **I want** AI prompts to include explicit boundary instructions **so that** the AI knows what it cannot do.

**Acceptance Criteria:**
- Given a prompt is constructed
- When sent to the AI
- Then it includes explicit "DO NOT" instructions for state modification

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-006

---

### STORY-046: Context Injection
**As an** admin, **I want** game state context included in AI prompts **so that** responses are accurate to the current situation.

**Acceptance Criteria:**
- Given the AI generates a description
- When the prompt is built
- Then it includes: current location, player stats, nearby NPCs/items, time of day

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-006

---

## Player System (FEAT-007)

### STORY-047: Random Character Creation
**As a** player, **I want** to generate a random character **so that** I can start playing quickly.

**Acceptance Criteria:**
- Given I select "Random Character"
- When creation completes
- Then I have a character with randomized stats and background

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-007

---

### STORY-048: Custom Character Creation
**As a** player, **I want** to customize my character's stats **so that** I can play my preferred build.

**Acceptance Criteria:**
- Given I select "Custom Character"
- When I allocate stat points
- Then my character has the stats I chose within valid ranges

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-007

---

### STORY-049: Stat Display
**As a** player, **I want** to view my character's stats **so that** I can make informed decisions.

**Acceptance Criteria:**
- Given I type "stats" or "character"
- When the command executes
- Then I see: strength, agility, intelligence, health, mana, armor

**Story Points:** 2  
**Priority:** P1  
**Related Feature:** FEAT-007

---

### STORY-050: Stat Modifiers
**As a** player, **I want** equipment to modify my stats **so that** gear choices matter.

**Acceptance Criteria:**
- Given I equip a +2 strength sword
- When I check my stats
- Then my strength displays the base value plus the modifier

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-007

---

### STORY-051: Action Command Mapping
**As a** player, **I want** my commands to map to character actions **so that** I can interact with the world.

**Acceptance Criteria:**
- Given I type "attack goblin"
- When the command is processed
- Then it resolves to the attack action using my combat stats

**Story Points:** 3  
**Priority:** P1  
**Related Feature:** FEAT-007

---

### STORY-052: Skill Commands
**As a** player, **I want** to use special abilities **so that** combat has tactical options.

**Acceptance Criteria:**
- Given I have learned a skill
- When I type "use [skill] [target]"
- Then the skill executes with appropriate effects and cooldowns

**Story Points:** 5  
**Priority:** P3  
**Related Feature:** FEAT-007

---

### STORY-053: Level Progression
**As a** player, **I want** to gain experience and level up **so that** my character grows stronger.

**Acceptance Criteria:**
- Given I gain enough XP to level up
- When the threshold is crossed
- Then I gain stat improvements and possibly new abilities

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-007

---

## Game Modes (FEAT-008)

### STORY-054: Game Mode Selection
**As a** player, **I want** to choose between Story Mode and Random World **so that** I can pick my preferred experience.

**Acceptance Criteria:**
- Given I start a new game
- When presented with mode options
- Then I can select Story Mode (narrative-driven) or Random World (procedural)

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-055: Setup Wizard Flow
**As a** player, **I want** a guided setup process **so that** I can configure my game easily.

**Acceptance Criteria:**
- Given I start a new game
- When going through setup
- Then I'm prompted for: mode, character creation, difficulty, rule options

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-056: Save Game Slots
**As a** player, **I want** multiple save slots **so that** I can have several adventures running.

**Acceptance Criteria:**
- Given I type "save"
- When prompted for a slot
- Then I can choose from available slots and name my save

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-057: Save Listing
**As a** player, **I want** to see my available saves **so that** I can choose which to load.

**Acceptance Criteria:**
- Given I type "saves" or select load game
- When the list displays
- Then I see all saves with: name, date, character name, location

**Story Points:** 2  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-058: Auto-Save
**As a** player, **I want** the game to auto-save at key points **so that** I don't lose progress on crash.

**Acceptance Criteria:**
- Given I complete a major event or rest
- When the auto-save triggers
- Then my progress is saved to the auto-save slot

**Story Points:** 3  
**Priority:** P3  
**Related Feature:** FEAT-008

---

### STORY-059: Difficulty Selection
**As a** player, **I want** to choose difficulty (Easy/Normal/Hard) **so that** the challenge suits me.

**Acceptance Criteria:**
- Given I'm in setup
- When I select difficulty
- Then game parameters adjust: enemy scaling, resource scarcity, permadeath options

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-060: Rule Configuration
**As a** player, **I want** to toggle optional rules **so that** I can customize my experience.

**Acceptance Criteria:**
- Given I'm in advanced setup
- When configuring rules
- Then I can toggle: permadeath, magic scarcity, technology level

**Story Points:** 3  
**Priority:** P3  
**Related Feature:** FEAT-008

---

### STORY-061: Story Mode Preset
**As a** player, **I want** Story Mode with pre-written narrative **so that** I can experience crafted quests.

**Acceptance Criteria:**
- Given I select Story Mode
- When the game starts
- Then I'm placed in a designed world with story nodes and quest chains

**Story Points:** 5  
**Priority:** P2  
**Related Feature:** FEAT-008

---

### STORY-062: Random World Preset
**As a** player, **I want** a fully procedural world **so that** every playthrough is unique.

**Acceptance Criteria:**
- Given I select Random World
- When the game starts
- Then a new world is generated with random layout, NPCs, and items

**Story Points:** 3  
**Priority:** P2  
**Related Feature:** FEAT-008

---

## Summary Statistics

| Feature | Story Count | Total Points | Priority |
|---------|-------------|--------------|----------|
| Core Engine | 8 | 27 | P1 |
| World System | 8 | 27 | P1/P2 |
| Entity System | 8 | 22 | P1/P2 |
| Combat System | 8 | 30 | P1/P2 |
| Story System | 7 | 21 | P2 |
| AI Narrative | 7 | 29 | P1/P2 |
| Player System | 7 | 26 | P1/P2 |
| Game Modes | 9 | 30 | P2/P3 |
| **TOTAL** | **62** | **232** | - |

---

## Priority Breakdown

| Priority | Count | Points |
|----------|-------|--------|
| P1 - Critical | 20 | 68 |
| P2 - High | 33 | 131 |
| P3 - Medium | 9 | 33 |

---

## Story Points Distribution

| Points | Count | Description |
|--------|-------|-------------|
| 1 | 1 | Very simple tasks |
| 2 | 7 | Simple tasks |
| 3 | 36 | Standard complexity |
| 5 | 17 | Complex tasks |
| 8 | 1 | Very complex tasks |
| 13 | 0 | Epic tasks (break down further) |
