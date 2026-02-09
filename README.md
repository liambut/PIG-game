# 🎮 PIG-Game

**Procedural Intelligent Game** — An AI-driven MUD (Multi-User Dungeon) with interactive fiction elements.

> *"Where deterministic systems meet limitless imagination."*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?logo=node.js)](https://nodejs.org/)

---

## 📖 What is PIG-Game?

PIG-Game is a revolutionary text-based adventure that combines the reliability of deterministic game engines with the creative power of AI storytelling. Unlike traditional text adventures with fixed narratives, PIG-Game uses AI to generate rich, dynamic descriptions and dialogue while maintaining strict game state integrity through a deterministic core.

### Philosophy

**Deterministic Engine, Narrative AI.**

The game world operates on predictable, testable rules — combat calculations, inventory management, and world state are handled by code. The AI's role is purely creative: painting vivid scenes, crafting compelling dialogue, and weaving narrative hooks that make each playthrough unique.

---

## ✨ Core Features

### 🧠 Deterministic Game Engine
- **Predictable Mechanics**: Combat, movement, and item interactions follow strict, testable rules
- **State Integrity**: Game state is never modified by AI — only by validated player actions
- **Canonical Command System**: All inputs normalized to a defined set of actions

### 🤖 AI Narrative Layer
- **Dynamic Descriptions**: Every location, NPC, and item gets rich, context-aware prose
- **Intelligent Dialogue**: NPCs converse naturally while staying true to their character
- **Procedural Storytelling**: Quest hooks and narrative threads woven dynamically into the world

### 🏰 MUD-Style Exploration
- **Tile-Based World**: Navigate a procedural world of interconnected locations
- **Interactive NPCs**: Talk, trade, fight, or befriend the inhabitants
- **Item Discovery**: Find, examine, and use items throughout your journey

### 🎲 Procedural Generation
- **Random Worlds**: Each playthrough generates a unique world layout
- **Story-Driven Mode**: Structured narratives with procedural elements
- **Character Creation**: Choose random generation or custom builds

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         PIG-Game Architecture                    │
└─────────────────────────────────────────────────────────────────┘

  ┌──────────────┐     ┌─────────────────────┐     ┌──────────────┐
  │  Player      │────▶│  Command            │────▶│  Canonical   │
  │  Input       │     │  Normalization      │     │  Action      │
  └──────────────┘     └─────────────────────┘     └──────────────┘
                                                            │
                                                            ▼
  ┌──────────────┐     ┌─────────────────────┐     ┌──────────────┐
  │  AI          │◀────│  World/State        │◀────│  Deterministic│
  │  Narrative   │     │  Persistence        │     │  Game Engine  │
  └──────────────┘     └─────────────────────┘     └──────────────┘
         │
         ▼
  ┌──────────────┐
  │  Player      │
  │  Response    │
  └──────────────┘
```

### Data Models

**Tile**
```typescript
{
  id: string;
  type: 'forest' | 'dungeon' | 'town' | ...;
  description: string;
  npcs: NPC[];
  items: Item[];
  connections: { north?: string; south?: string; east?: string; west?: string };
  storyHooks: StoryHook[];
}
```

**NPC/Enemy**
```typescript
{
  id: string;
  name: string;
  type: 'merchant' | 'guard' | 'monster' | ...;
  health: number;
  armor: number;
  status: StatusEffect[];
  location: string; // tile id
}
```

**Player**
```typescript
{
  health: number;
  mana: number;
  inventory: Item[];
  position: string; // tile id
  stats: { strength: number; agility: number; intelligence: number; ... };
}
```

---

## 🚀 Quickstart Guide

### Start the Game
```bash
npm start
```

### Choose Your Adventure
1. **Story Mode** — Embark on a structured narrative with procedural elements
2. **Random World** — Dive into a completely generated world

### Character Creation
- **Random** — Let fate decide your starting stats and background
- **Custom** — Manually allocate stats and choose your origin

### Set Your Challenge
- **Easy** — For those who want to explore the story
- **Normal** — Balanced combat and resource management
- **Hard** — Every decision matters, resources are scarce

### Configure Rules
- **Permadeath** — One life. Make it count.
- **Magic Scarcity** — How rare are magical items and abilities?
- **Technology Level** — From medieval fantasy to steampunk

---

## 🛠️ Setup Instructions

### Prerequisites
- [Node.js](https://nodejs.org/) 18 or higher
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- An AI API key (OpenAI, Anthropic, or compatible)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/liambut/PIG-game.git
   cd PIG-game
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys and preferences
   ```

4. **Run the game**
   ```bash
   npm start
   ```

### Development

```bash
# Run in development mode with hot reload
npm run dev

# Run tests
npm test

# Build for production
npm run build
```

---

## 🤝 AI Usage Contract

To maintain game integrity while leveraging AI creativity, we establish strict boundaries:

### ✅ AI May:
- **Describe the world** — Generate vivid location descriptions and atmospheric details
- **Write dialogue** — Create character voices and conversational responses
- **Add flavor text** — Enrich items, actions, and events with narrative detail
- **Suggest story hooks** — Propose narrative threads and quest ideas

### ❌ AI May Not:
- **Modify stats** — Never change player or NPC health, mana, or attributes
- **Manage inventory** — Cannot add, remove, or modify items
- **Move the player** — Location changes require explicit player commands
- **Spawn entities** — No creating NPCs, items, or enemies
- **Resolve quests** — Quest state changes only through validated game logic
- **Determine combat outcomes** — AI describes; the engine decides damage and death

This contract ensures that while the AI brings the world to life with words, the **game engine alone** governs the rules of reality.

---

## 🎯 Main Game Loop

```
┌─────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  Read   │───▶│ Normalize│───▶│ Validate │───▶│ Execute  │
│  Input  │    │ Command  │    │  Action  │    │  Action  │
└─────────┘    └──────────┘    └──────────┘    └──────────┘
                                                      │
       ┌──────────────────────────────────────────────┘
       ▼
┌──────────┐    ┌──────────┐    ┌──────────┐
│ Persist  │───▶│ Generate │───▶│  Output  │
│  State   │    │Narrative │    │ Response │
└──────────┘    └──────────┘    └──────────┘
```

---

## 📝 Contributing

We welcome contributions! Here's how to get started:

### Development Setup

1. **Fork and clone**
   ```bash
   git clone https://github.com/YOUR_USERNAME/PIG-game.git
   cd PIG-game
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Make your changes**
   - Follow the existing code style
   - Add tests for new functionality
   - Update documentation as needed

5. **Test your changes**
   ```bash
   npm test
   npm run build  # Must pass without errors
   ```

6. **Commit and push**
   ```bash
   git add .
   git commit -m "feat: Add your feature description"
   git push origin feature/your-feature-name
   ```

7. **Open a Pull Request**

### Contribution Guidelines

- **Issues**: Check existing issues before creating new ones
- **Commits**: Use conventional commit format (`feat:`, `fix:`, `docs:`, etc.)
- **Tests**: All new features should include tests
- **Documentation**: Update README.md if your change affects usage
- **AI Contract**: Any changes to AI interaction must respect the Usage Contract

### Code Style

- TypeScript with strict mode enabled
- Functions should be under 20 lines when possible
- Single responsibility principle
- No magic numbers — use named constants
- Handle errors explicitly (no swallowed exceptions)

---

## 📜 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Inspired by classic MUDs and interactive fiction
- Built with modern AI language models
- Community-driven development

---

<p align="center">
  <strong>Enter the world. Write your story.</strong><br>
  <em>Every adventure is unique. Every choice matters.</em>
</p>
