# Legends of the Wild - Codebase Guide

## Quick Overview
This is a classroom RPG game where students collect and battle creatures. The entire game is a single HTML file with embedded CSS and JavaScript.

**Current Version:** v54.15 | **Total Lines:** ~17,400

## File Structure
```
Legends_of_the_Wild_v54.html  - Main game file (~17,400 lines)
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

### CSS Sections (Lines 1-6320)
| Line Range | Section |
|------------|---------|
| 10-46 | Base Styles - Warm Amber/Sunset Theme |
| 47-232 | Creature Cards - Per-Card Element Theming |
| 233-420 | Idle Creature Animations - Element-specific |
| 380-392 | Mini Stats (HP/ATK/DEF/SPD/INT) with colors |
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
| 5810-6320 | Battle Items, Item Animations, Error Feedback |

### JavaScript Sections (Lines 6320+)
| Line Range | Section | Key Functions/Data |
|------------|---------|-------------------|
| 6334-6470 | Audio System | `initAudio()`, `playSound()`, `playMusic()` |
| 6473-6685 | Party Scaling System | `getPartySize()`, `PARTY_SCALING`, `scaleWildEnemy()`, `scaleBoss()` |
| 7192-7210 | Focus System Constants | `STARTING_FOCUS`, `MAX_FOCUS`, `BASE_FOCUS_REGEN`, `INT_FOCUS_MODIFIER`, `calculateFocusRegen()` |
| 7217-7260 | **NATURES Object** | 25 natures including 4 INT-focused (wise, sage, clever, scholarly) |
| 7260-7305 | Nature Functions | `getNatureCategory()`, `getRandomNature()`, `formatNatureEffects()` |
| 7305-7320 | Special Cost Calculation | `calculateSpecialCost()` |
| 7320-7450 | Enemy Damage & AOE | `adjustEnemyDamage()`, `getSpecialType()`, `ELEMENT_EMOJI` |
| 7450-7870 | Shop System | `SHOP_ITEMS`, `REAL_REWARDS`, `CLASSROOM_REWARDS` |
| 7900-7970 | **CREATURES Object** | All 22 player creatures with INT stats |
| 7970-8200 | **WILD_ENCOUNTERS** | Wild creatures by region |
| 8200-8250 | **MINIONS / BOSS_MINIONS** | Minion definitions |
| 8250-8300 | **BOSSES Object** | All boss definitions by tier |
| 8300-8450 | **CHAPTERS Object** | Story chapters, progression |
| 8450-8500 | **XP_TABLE** | Level thresholds (1-50) |
| 8500-8550 | **Game State (`state`)** | Main state object |
| 8660-8700 | Utility Functions | `getLv()`, `getEvo()`, `getStats()`, `getImg()`, `getMove()` |
| 8700-8850 | Boss/Chapter Logic | `canFightBoss()`, `isTierComplete()`, `getCurrentChapter()` |
| 8850-9050 | Shop/Migration | `migrateShopSystem()`, migrations |
| 9050-9700 | **Arena PvP System** | `ARENA_MODES`, `renderArena()`, arena battle |
| 9700-10500 | Render Functions | `renderMain()`, `renderNav()`, `renderParty()`, `renderShop()` |
| 10500-11300 | Adventure System | `renderAdventure()`, `startAdventure()`, `startWildEncounter()` |
| 11300-12500 | Boss Encounters | `startBossEncounter()`, `spawnBossMinions()` |
| 12500-13300 | Battle Setup | `startBattleWith()`, `buildTurnOrder()` |
| 13300-13900 | Battle Rendering | `nextTurn()`, `renderBattle()` |
| 13900-14900 | **doAction() & Combat** | Main combat handler |
| 14900-15500 | Animation Effects | `fireProjectile()`, `showSlashEffect()`, `showImpactEffect()` |
| 15500-16300 | Target Selection | `selectTarget()`, `selectHealTarget()`, `executeHeal()` |
| 16300-16900 | **Enemy AI** | `enemyAction()`, `executeEnemyHeal()` |
| 16900-17200 | Victory/Defeat | `endBattle()`, `showVictoryOverlay()`, `showDefeatOverlay()` |
| 17200-17450 | Level Up/Evolution | `showNextLevelUp()`, `showEvolutionSequence()` |
| 17450-17520 | Save/Load, Init | `save()`, `load()`, `resetGame()` |

## Key Global Objects
- `state` - Main game state (party, inventory, coins, chapter, etc.)
- `CREATURES` - All creature definitions with stats (HP/ATK/DEF/SPD/INT) and evolutions (~7900)
- `BOSSES` - Boss definitions (~8250)
- `CHAPTERS` - Chapter/region definitions (~8300)
- `WILD_ENCOUNTERS` - Regional wild creature spawn tables (~7970)
- `MINIONS` / `BOSS_MINIONS` - Minion definitions (~8200)
- `NATURES` - Creature personality modifiers with INT (~7217)
- `SHOP_ITEMS` / `REAL_REWARDS` - Shop item definitions (~7450)
- `PARTY_SCALING` - Enemy stat multipliers by party size (~6521)

## Stats System (v54.15)
The game has **5 core stats**:
- **HP** (Health Points) - Red (#f87171)
- **ATK** (Attack) - Gold (#fbbf24)
- **DEF** (Defense) - Blue (#60a5fa)
- **SPD** (Speed) - Green (#4ade80)
- **INT** (Intelligence) - Purple (#c084fc) - NEW in v54.15

### INT Stat Effects
- **Healing Power**: +0.8% per INT point (INT 10 = +8%, INT 30 = +24%)
- **Focus Regen**: Base 5 + (INT × 0.15) per turn
  - INT 10 = 6 focus/turn
  - INT 20 = 8 focus/turn
  - INT 30 = 9 focus/turn

### INT Values by Creature Type
| Type | Base INT | Description |
|------|----------|-------------|
| Light | 22-24 | Best healers, divine |
| Void | 24 | Psychic/mental |
| Nature | 18-20 | Natural wisdom |
| Shadow | 18-20 | Cunning |
| Water/Ice | 16-18 | Elemental wisdom |
| Lightning | 14-16 | Quick-witted |
| Fire | 12-14 | Low support |
| Earth/Metal/Bug | 10-12 | Physical focus |
| Mythical (Rúnvíg) | 30 | Divine special |

## Common Edit Locations

### To modify creature stats/abilities:
- `CREATURES` object (~line 7900)

### To modify boss encounters:
- `BOSSES` object (~line 8250)
- `startBossEncounter()` (~line 11300)

### To modify battle mechanics:
- `doAction()` (~line 13900) - Main combat action handler
- `enemyAction()` (~line 16300) - Enemy AI
- Party scaling in `PARTY_SCALING` (~line 6521)
- Damage adjustment in `adjustEnemyDamage()` (~line 7350)

### To modify UI/styling:
- CSS is at the top of the file (lines 1-6320)
- Render functions start around line 9700
- Battle UI in `renderBattle()` (~line 13500)

### To modify shop/items:
- `SHOP_ITEMS` array (~line 7460) contains all items
- `REAL_REWARDS` array (~line 7680)
- Shop render at `renderShop()` (~line 9900)

### To modify nature system:
- `NATURES` object (~line 7217) - includes INT modifiers
- 4 INT-focused natures: wise, sage, clever, scholarly
- Nature applied in `getStats()` (~line 8667)

### To modify INT/focus regen:
- Constants at ~line 7200: `BASE_FOCUS_REGEN`, `INT_FOCUS_MODIFIER`
- `calculateFocusRegen(int)` helper function (~line 7207)
- Healing INT bonus in `showHealTargetSelection()` (~line 18497)

## Tips for Efficient Editing

1. **Use line numbers** - Ask Claude to read specific line ranges rather than the whole file
2. **Be specific** - "Edit the `doAction` function around line 13900" is better than "fix combat"
3. **One change at a time** - Make focused, targeted edits
4. **Reference this guide** - Point Claude to specific sections listed above
5. **Skip asset folders** - These only contain images, don't explore them

## For Full Reference

See `CLAUDE_PROMPT.md` for a comprehensive prompt document that includes:
- Complete data structure documentation
- All game mechanics explanations
- Battle system details
- Nature system details (including INT)
- Boss progression system

## Recent Changes (v54.15)
- Added INT (Intelligence) stat to all creatures
- INT affects healing power (+0.8% per point)
- INT affects focus regeneration (base 5 + INT×0.15)
- Added 4 new INT-focused natures: wise, sage, clever, scholarly
- Updated UI to display INT with 🧠 emoji in purple
