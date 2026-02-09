# PIG-Game
**Procedural Intelligent Game (AI-driven MUD / Interactive Fiction)**

## Core Design Principles
1. Deterministic Engine, Narrative AI
2. No Meta Commands
3. Procedural but Logical

## High-Level System Architecture
Player Input → Command Normalization Layer → Canonical Action Object → Deterministic Game Engine → World/State Persistence → AI Narrative Layer → Player Response

## Game Start Flow
- Story Mode (Random World / Story-Driven)
- Character Creation (Random / Custom)
- Difficulty (Easy/Normal/Hard)
- Rules (Permadeath, Magic scarcity, Technology level)

## World Model
- Tile (id, type, description, npcs, items, connections, story hooks)
- NPC/Enemy (id, name, type, health, armor, status, location)
- Player (health, mana, inventory, position, stats)

## Command Normalization Pipeline
Canonical Commands: move_north/south/east/west, look, examine, take, use, talk, attack

## Deterministic Combat System
AI describes outcome only, never modifies numeric values

## Story System
Story nodes (quest, event, arc) attach to tiles/NPCs/items

## AI Usage Contract
AI May: Describe world, write dialogue, add flavor, suggest hooks
AI May Not: Modify stats, inventory, move player, spawn entities, resolve quests

## Main Game Loop
Read input → Normalize → Validate → Execute → Persist → Generate narrative → Output
