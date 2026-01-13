# Legends of the Wild - Codebase Guide

## Quick Overview
This is a classroom RPG game where students collect and battle creatures. The entire game is a single HTML file with embedded CSS and JavaScript.

## File Structure
```
Legends_of_the_Wild_v54.html  - Main game file (13,472 lines)
Player_Creatures/             - Player creature sprite images
Bosses/                       - Boss sprite images
Minions/                      - Minion sprite images
Wild_Encounters/              - Wild encounter sprite images
Backgrounds/                  - Battle background images
Environments/                 - Environment images
Quest_Creatures/              - Quest creature images
UI_Elements/                  - UI element images
TheCreator/                   - Special NPC images
```

## Main File Structure (Legends_of_the_Wild_v54.html)

### CSS Sections (Lines 1-4600)
| Line Range | Section |
|------------|---------|
| 10-46 | Base Styles - Warm Amber/Sunset Theme |
| 47-232 | Creature Cards - Per-Card Element Theming |
| 233-420 | Idle Creature Animations - Element-specific |
| 421-516 | Other UI Components |
| 517-873 | Battle Screen - Combat Arena Styles |
| 874-1064 | Combat UI - Premium Fantasy RPG HUD |
| 1065-1400 | Move Buttons, Party Display |
| 1401-1993 | Combat Animations, Projectiles, Impact Effects |
| 1994-2689 | Action Banner, Level Up, Evolution Sequences |
| 2690-3029 | Screen Transitions |
| 3030-4600 | Shop, Inventory, Battle Items Systems |

### JavaScript Sections (Lines 4600+)
| Line Range | Section | Key Functions/Data |
|------------|---------|-------------------|
| 4675-4809 | Audio System | `initAudio()`, `playSound()`, `playMusic()` |
| 4810-5030 | Party Scaling System | `getPartySize()`, `scaleWildEnemy()`, `scaleBoss()` |
| 5031-5108 | Focus System | `STARTING_FOCUS`, `MAX_FOCUS` constants |
| 5037-5108 | Nature System | `NATURES` object, `getNatureCategory()` |
| 5109-5225 | Special Cost Calculation | `calculateSpecialCost()` |
| 5192-5251 | AOE/Element Detection | `getSpecialType()`, `ELEMENT_EMOJI` |
| 5252-5671 | Shop System | `RARITY` object with items/rewards |
| 5672-5699 | Creatures Data | `CREATURES` object |
| 5700-5932 | Wild Encounters | `WILD_ENCOUNTERS` by region |
| 5933-6021 | Minions/Boss Minions | `MINIONS`, `BOSS_MINIONS` objects |
| 5985-6200 | Bosses & Chapters | `BOSSES`, `CHAPTERS` objects |
| 6200-8000 | Render Functions | `renderMain()`, `renderParty()`, `renderShop()` |
| 8000-9000 | Arena/PvP System | `renderArena()`, `startArenaBattle()` |
| 9000-10000 | Adventure/Encounters | `startAdventure()`, `startWildEncounter()` |
| 10000-11100 | Boss Encounters | `startBossEncounter()`, `spawnBossMinions()` |
| 11100-11200 | Events | `treasureEvent()`, `specialEvent()`, `creatorBlessingEvent()` |
| 11200-12000 | Battle System | `startBattleWith()`, `nextTurn()`, `renderBattle()`, `doAction()` |
| 12000-12400 | Battle Animations | `fireProjectile()`, `showSlashEffect()`, `showImpactEffect()` |
| 12400-12900 | Target Selection/Healing | `selectTarget()`, `selectHealTarget()`, `executeHeal()` |
| 12900-13100 | Enemy AI | `enemyAction()`, `executeEnemyHeal()` |
| 13100-13400 | Victory/Defeat | `endBattle()`, `showVictoryOverlay()`, `showDefeatOverlay()` |
| 13400-13472 | Save/Load, Init | `saveGame()`, `loadGame()`, `resetGame()` |

## Key Global Objects
- `state` - Main game state (party, inventory, coins, chapter, etc.)
- `CREATURES` - All creature definitions with stats and evolutions
- `BOSSES` - Boss definitions
- `CHAPTERS` - Chapter/region definitions
- `WILD_ENCOUNTERS` - Regional wild creature spawn tables
- `MINIONS` / `BOSS_MINIONS` - Minion definitions
- `NATURES` - Creature personality modifiers
- `RARITY` - Shop item definitions

## Common Edit Locations

### To modify creature stats/abilities:
- `CREATURES` object (~line 5672)

### To modify boss encounters:
- `BOSSES` object (~line 5985)
- `startBossEncounter()` (~line 10076)

### To modify battle mechanics:
- `doAction()` (~line 11604) - Main combat action handler
- `enemyAction()` (~line 12549) - Enemy AI
- Party scaling in `PARTY_SCALING` (~line 4858)

### To modify UI/styling:
- CSS is at the top of the file (lines 1-4600)
- Render functions start around line 6200

### To modify shop/items:
- `RARITY` object (~line 5252) contains all items
- Shop render at `renderShop()`

## Tips for Efficient Editing

1. **Use line numbers** - Ask Claude to read specific line ranges rather than the whole file
2. **Be specific** - "Edit the `doAction` function around line 11604" is better than "fix combat"
3. **One change at a time** - Make focused, targeted edits
4. **Reference this guide** - Point Claude to specific sections listed above
