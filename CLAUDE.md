# Legends of the Wild - Codebase Guide

## Quick Overview
This is a classroom RPG game where students collect and battle creatures. The entire game is a single HTML file with embedded CSS and JavaScript.

**Current Version:** v54.8 | **Total Lines:** ~17,320

## File Structure
```
Legends_of_the_Wild_v54.html  - Main game file (~17,320 lines)
Player_Creatures/             - Player creature sprite images
Bosses/                       - Boss sprite images (organized by tier)
Minions/                      - Minion sprite images
Wild_Encounters/              - Wild encounter sprite images (by region)
Backgrounds/                  - Battle background images
Environments/                 - Environment images
Quest_Creatures/              - Quest creature images
UI_Elements/                  - UI element images
TheCreator/                   - Special NPC images (Mr. Gabe)
```

## Main File Structure (Legends_of_the_Wild_v54.html)

### CSS Sections (Lines 1-6318)
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
| 3030-4600 | Shop, Inventory Systems |
| 4600-5200 | Arena Battle Styles |
| 5200-5580 | Arena Victory, Responsive |
| 5580-5810 | Inventory Modal Styles |
| 5810-6318 | Battle Items, Item Animations, Error Feedback |

### JavaScript Sections (Lines 6320+)
| Line Range | Section | Key Functions/Data |
|------------|---------|-------------------|
| 6334-6470 | Audio System | `initAudio()`, `playSound()`, `playMusic()` |
| 6473-6685 | Party Scaling System | `getPartySize()`, `PARTY_SCALING`, `scaleWildEnemy()`, `scaleBoss()` |
| 6688-6694 | Focus System Constants | `STARTING_FOCUS`, `MAX_FOCUS`, `BASE_SPECIAL_COST` |
| 6696-6776 | Nature System | `NATURES` object, `getNatureCategory()` |
| 6778-6810 | Special Cost Calculation | `calculateSpecialCost()` |
| 6812-6946 | Enemy Damage & AOE | `adjustEnemyDamage()`, `getSpecialType()`, `ELEMENT_EMOJI` |
| 6948-7370 | Shop System | `SHOP_ITEMS`, `REAL_REWARDS`, `CLASSROOM_REWARDS` |
| 7373-7442 | **CREATURES Object** | All player creature definitions |
| 7447-7676 | **WILD_ENCOUNTERS** | Wild creatures by region |
| 7678-7730 | **MINIONS / BOSS_MINIONS** | Minion definitions |
| 7732-7766 | **BOSSES Object** | All boss definitions by tier |
| 7768-7950 | **CHAPTERS Object** | Story chapters, progression |
| 7898-7949 | **XP_TABLE** | Level thresholds (1-50) |
| 7951-7990 | **Game State (`state`)** | Main state object |
| 7992-8070 | Utility Functions | `getLv()`, `getEvo()`, `getStats()`, `getImg()`, `getMove()` |
| 8070-8200 | Boss/Chapter Logic | `canFightBoss()`, `isTierComplete()`, `getCurrentChapter()` |
| 8200-8420 | Shop/Migration | `migrateShopSystem()`, migrations |
| 8420-9400 | **Arena PvP System** | `ARENA_MODES`, `renderArena()`, arena battle |
| 9400-10200 | Render Functions | `renderMain()`, `renderNav()`, `renderParty()`, `renderShop()` |
| 10200-11000 | Adventure System | `renderAdventure()`, `startAdventure()`, `startWildEncounter()` |
| 11000-12200 | Boss Encounters | `startBossEncounter()`, `spawnBossMinions()` |
| 12200-13000 | Battle Setup | `startBattleWith()`, `buildTurnOrder()` |
| 13000-13600 | Battle Rendering | `nextTurn()`, `renderBattle()` |
| 13600-14600 | **doAction() & Combat** | Main combat handler |
| 14600-15200 | Animation Effects | `fireProjectile()`, `showSlashEffect()`, `showImpactEffect()` |
| 15200-16000 | Target Selection | `selectTarget()`, `selectHealTarget()`, `executeHeal()` |
| 16000-16600 | **Enemy AI** | `enemyAction()`, `executeEnemyHeal()` |
| 16600-16830 | Victory/Defeat | `endBattle()`, `showVictoryOverlay()`, `showDefeatOverlay()` |
| 16830-17150 | Level Up/Evolution | `showNextLevelUp()`, `showEvolutionSequence()` |
| 17150-17207 | Save/Load, Init | `save()`, `load()`, `resetGame()` |

## Key Global Objects
- `state` - Main game state (party, inventory, coins, chapter, etc.)
- `CREATURES` - All creature definitions with stats and evolutions (~7373)
- `BOSSES` - Boss definitions (~7732)
- `CHAPTERS` - Chapter/region definitions (~7768)
- `WILD_ENCOUNTERS` - Regional wild creature spawn tables (~7447)
- `MINIONS` / `BOSS_MINIONS` - Minion definitions (~7678)
- `NATURES` - Creature personality modifiers (~6696)
- `SHOP_ITEMS` / `REAL_REWARDS` - Shop item definitions (~6948)
- `PARTY_SCALING` - Enemy stat multipliers by party size (~6521)

## Common Edit Locations

### To modify creature stats/abilities:
- `CREATURES` object (~line 7373)

### To modify boss encounters:
- `BOSSES` object (~line 7732)
- `startBossEncounter()` (~line 11000)

### To modify battle mechanics:
- `doAction()` (~line 13600) - Main combat action handler
- `enemyAction()` (~line 16000) - Enemy AI
- Party scaling in `PARTY_SCALING` (~line 6521)
- Damage adjustment in `adjustEnemyDamage()` (~line 6839)

### To modify UI/styling:
- CSS is at the top of the file (lines 1-6318)
- Render functions start around line 9400
- Battle UI in `renderBattle()` (~line 13247)

### To modify shop/items:
- `SHOP_ITEMS` array (~line 6962) contains all items
- `REAL_REWARDS` array (~line 7176)
- Shop render at `renderShop()` (~line 9600)

### To modify nature system:
- `NATURES` object (~line 6696)
- Nature applied in `getStats()` (~line 7997)

## Tips for Efficient Editing

1. **Use line numbers** - Ask Claude to read specific line ranges rather than the whole file
2. **Be specific** - "Edit the `doAction` function around line 13600" is better than "fix combat"
3. **One change at a time** - Make focused, targeted edits
4. **Reference this guide** - Point Claude to specific sections listed above
5. **Skip asset folders** - These only contain images, don't explore them

## For Full Reference

See `CLAUDE_PROMPT.md` for a comprehensive prompt document that includes:
- Complete data structure documentation
- All game mechanics explanations
- Battle system details
- Nature system details
- Boss progression system
