# Legends of the Wild - Complete Claude Code Reference

**Version:** v54.7 | **Lines:** ~17,207 | **Last Updated:** January 2026

Copy and paste this entire document at the start of each new Claude Code session to provide full context without reading the massive HTML file.

---

## CRITICAL RULES FOR CLAUDE CODE

### 1. NEVER Read the Full HTML File
The main file `Legends_of_the_Wild_v54.html` is ~17,207 lines. **Always read specific line ranges:**
```
Good: Read lines 13500-13600 from Legends_of_the_Wild_v54.html
Bad:  Read Legends_of_the_Wild_v54.html
```

### 2. Skip Asset Directories (Images Only)
Never explore these folders - they only contain PNG images:
- `Player_Creatures/`, `Bosses/`, `Minions/`, `Wild_Encounters/`
- `Backgrounds/`, `Environments/`, `Quest_Creatures/`, `UI_Elements/`, `TheCreator/`

### 3. Make Surgical Edits
- Read only the specific function you need to modify
- Use the Edit tool with precise `old_string` matching
- Don't rewrite large sections unnecessarily

---

## GAME OVERVIEW

**Legends of the Wild** is a classroom RPG where students collect and battle creatures. It's a single HTML file with embedded CSS and JavaScript.

### Core Gameplay Loop
1. **Students** are assigned creature IDs (e.g., `lightning_wolf`, `fire_raptor`)
2. **Adventures** trigger wild encounters or boss battles
3. **Battles** are turn-based with ATK/DEF/HEAL/SPECIAL actions
4. **XP/Coins** are earned from victories, used for leveling and shop purchases
5. **Evolution** occurs at level thresholds (creature sprites change)
6. **Boss Progression** unlocks chapters (Tier 1 → Nightmare P0 → Tier 2 → etc.)

---

## FILE STRUCTURE - LINE NUMBER REFERENCE

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
| 6334-6470 | Audio System | `initAudio()`, `playSound()`, `playMusic()`, `stopMusic()` |
| 6473-6685 | Party Scaling System | `getPartySize()`, `getPartyTier()`, `PARTY_SCALING`, `scaleWildEnemy()`, `scaleBoss()` |
| 6688-6810 | Focus System Constants | `STARTING_FOCUS=25`, `FOCUS_REGEN_PER_TURN=10`, `MAX_FOCUS=100`, `BASE_SPECIAL_COST=35` |
| 6696-6776 | Nature System | `NATURES` object, `getNatureCategory()`, `getRandomNature()`, `formatNatureEffects()` |
| 6778-6810 | Special Cost Calculation | `calculateSpecialCost()` (dynamic based on evo/power/AOE) |
| 6812-6890 | Enemy Damage Adjustment | `adjustEnemyDamage()`, `getBuffValue()`, `getPartyShieldValue()` |
| 6892-6946 | AOE Detection | `getSpecialType()`, `ELEMENT_EMOJI` |
| 6948-7175 | Shop Items (SHOP_ITEMS) | Consumables, equipment by chapter |
| 7175-7370 | Real/Classroom Rewards | `REAL_REWARDS`, `CLASSROOM_REWARDS` |
| 7373-7442 | **CREATURES Object** | All player creature definitions |
| 7447-7676 | **WILD_ENCOUNTERS** | By region: forest, volcano, ice, void |
| 7678-7730 | **MINIONS / BOSS_MINIONS** | Minion definitions and boss mappings |
| 7732-7766 | **BOSSES Object** | All boss definitions by tier |
| 7768-7950 | **CHAPTERS Object** | Story chapters, regions, boss gates |
| 7898-7949 | **XP_TABLE** | Level thresholds (1-50) |
| 7951-7990 | **Game State (`state`)** | Main state object structure |
| 7992-8070 | Utility Functions | `getLv()`, `getXPProg()`, `getEvo()`, `getStats()`, `getImg()`, `getMove()` |
| 8070-8200 | Boss/Chapter Logic | `canFightBoss()`, `isTierComplete()`, `canFightNightmarePhase()`, `getCurrentChapter()` |
| 8200-8420 | Shop/Migration | `migrateShopSystem()`, `migrateToV54_1()`, `migrateToV54_3_Natures()` |
| 8420-8800 | **Arena PvP System** | `ARENA_MODES`, `renderArena()`, team selection |
| 8800-9400 | Arena Battle Functions | `startArenaBattle()`, arena combat logic |
| 9400-10200 | Render Functions | `renderMain()`, `renderNav()`, `renderParty()`, `renderShop()` |
| 10200-11000 | Adventure System | `renderAdventure()`, `startAdventure()`, `startWildEncounter()` |
| 11000-12200 | Boss Encounters | `startBossEncounter()`, `spawnBossMinions()`, events |
| 12200-13000 | Battle Setup | `startBattleWith()`, `buildTurnOrder()`, battle initialization |
| 13000-13600 | **Battle Rendering** | `nextTurn()`, `renderBattle()` |
| 13600-14600 | **doAction() & Combat** | Main combat handler, damage calculation, animations |
| 14600-15200 | Animation Effects | `fireProjectile()`, `showSlashEffect()`, `showImpactEffect()`, element effects |
| 15200-16000 | Target Selection | `selectTarget()`, `selectHealTarget()`, `executeHeal()` |
| 16000-16600 | **Enemy AI** | `enemyAction()`, `executeEnemyHeal()`, boss attack patterns |
| 16600-16830 | Victory/Defeat | `endBattle()`, `showVictoryOverlay()`, `showDefeatOverlay()` |
| 16830-17150 | Level Up/Evolution | `showNextLevelUp()`, `showEvolutionSequence()` |
| 17150-17207 | Save/Load, Init | `save()`, `load()`, `resetGame()`, DOMContentLoaded |

---

## KEY DATA STRUCTURES

### `state` - Main Game State (Line ~7951)
```javascript
state = {
    students: [],           // Array of student objects
    activeIds: [],          // IDs of students present today
    quests: {},
    totalXP: 0,
    defeated: [],           // Defeated boss IDs (e.g., ['sludge_king', 'nightmare_p0'])
    battle: null,           // Current battle state (null when not in battle)
    log: [],                // Battle log entries
    storyLog: [],           // Narrative log
    chapter: 1,             // Current chapter (1-5)
    adventureCount: 0,
    challengeLocked: false,
    introSeen: false,
    // Shop System
    shop: { unlockedChapter: 1, lastRefreshTs: Date.now() },
    shopConfig: { coinEconomyMultiplier: 1.0, ... },
    realRewardLog: [],
    shopLog: [],
    limitedTime: { nextResetAt: null, weeklyRewards: [] },
    classroomRewards: {},
    // Arena
    arenaMode: { enabled: false, records: {}, lastMatch: null },
    // Migrations
    migratedV54_1: true,
    migratedV54_3_Natures: true,
    bossesDefeated: { tier1: 0, tier2: 0, tier3: 0, tier4: 0, nightmare: 0 },
    discoveredCreatures: {}
}
```

### Student Object Structure
```javascript
student = {
    id: 1,                  // Unique ID
    name: "Alex",           // Student name
    cid: "lightning_wolf",  // Creature ID (key in CREATURES)
    xp: 500,                // Total XP (use getLv(xp) to get level)
    nature: "brave",        // Nature modifier (from NATURES)
    coins: 150,             // Personal coins
    inventory: {},          // {itemId: quantity}
    loadout: { charm: null, trinket: null },  // Equipped items
    xpBoostAdventures: 0,
    coinBoostAdventures: 0
}
```

### Creature Definition (CREATURES object, Line ~7373)
```javascript
CREATURES = {
    lightning_wolf: {
        name: "Lightning Wolf",
        type: "Lightning",
        evo: 2,                    // Max evolution stage (2 = 2 evolutions)
        evAt: [12],                // Levels where evolution occurs
        base: { hp: 70, atk: 30, def: 16, spd: 30 },
        grow: { hp: 13, atk: 5, def: 3, spd: 5 },  // Stats gained per level
        imgs: ["LightningWolf_Evo1.png", "LightningWolf_Evo2.png"],
        names: ["Spark Pup", "Thunder Wolf"],  // Evolution names
        canHeal: false,
        forcedNature: null,        // Only "runvig" has forcedNature: "godtouched"
        moves: {
            atk: [{ n: "Thunder Fang", lv: 1, p: 1, f: 0 }, { n: "Volt Tackle", lv: 10, p: 1.4, f: 0 }],
            def: [{ n: "Static Shield", lv: 1, f: 0 }],
            spec: [{ n: "Lightning Storm", lv: 8, p: 1.9, f: 30 }]
            // heal: [...] if canHeal is true
        }
    },
    // ... more creatures
}
```

### Boss Definition (BOSSES object, Line ~7732)
```javascript
BOSSES = {
    sludge_king: {
        name: "Sludge King",
        tier: 1,                   // Boss tier (1-5)
        lv: 15,                    // Boss level
        type: "Poison",
        weak: "Fire",              // Weakness element
        hp: 1000, atk: 55, def: 40, spd: 28,
        xp: 200, coins: 40,
        img: "Bosses/Tier 1/Boss_TheSludgeKing.png",
        bg: "Backgrounds_DarkForest.png",
        atks: { s: ["Toxic Slam", "Poison Claw"], a: ["Toxic Wave"] },  // s=single, a=aoe
        intro: "The swamp bubbles violently..."
    },
    // Tiers: 1 (5 bosses), 2 (3 bosses), 3 (4 bosses), 4 (nightmare phases 0-4), 5 (THE CREATOR)
}
```

### Battle State Structure (`state.battle`)
```javascript
state.battle = {
    team: [{                       // Array of party members in battle
        sid: 1,                    // Student ID
        cid: "lightning_wolf",
        name: "Alex",
        lv: 15,
        st: { hp: 200, atk: 80, def: 45, spd: 65 },  // Calculated stats
        maxHp: 200,
        curHp: 180,
        focus: 25,                 // Current focus points
        focusMax: 100,
        focusRegen: 10,
        cooldown: 0,               // Special cooldown (turns)
        healCooldown: 0,           // Heal cooldown (turns)
        buffs: [],                 // Active buffs [{type, value, turns}]
        nature: "brave"
    }],
    enemies: [{                    // Array of enemies
        name: "Sludge King",
        hp: 1000,
        maxHp: 1000,
        chipHp: 1000,              // For damage chip animation
        atk: 55, def: 40, spd: 28,
        lv: 15,
        img: "Bosses/Tier 1/...",
        isBoss: true,
        isMinion: false,
        tier: 1
    }],
    enemy: {...},                  // Primary enemy reference
    targetingMode: false,          // Attack target selection
    healTargetingMode: false,      // Heal target selection
    itemUsedThisTurn: {}           // {memberIdx: true} - tracks item usage
}
```

---

## GAME MECHANICS

### Combat System
- **Turn Order**: Based on SPD stat, higher goes first
- **Actions**: ATK (free), DEF (+10 Focus), HEAL (costs Focus, cooldown), SPECIAL (costs Focus, cooldown)
- **Focus**: Starts at 25, regenerates 10/turn, max 100
- **Special Costs**: Dynamic: `BASE_COST(35) + evo*5 + powerMod + aoeMod(15) + healMod(10)`, clamped 35-85
- **AOE Detection**: Keywords like "tsunami", "hurricane", "earthquake" in move names
- **AOE Damage**: 65% per target (balanced for hitting multiple enemies)

### Damage Calculation (approx)
```javascript
// Player Attack
damage = floor((atk * movePower - targetDef * 0.25) * randomRange(0.85, 1.15))

// Critical Hit
if (random < 0.10) damage *= 1.5

// Boss Devastating Blow
if (random < 0.12) damage *= getBossDevastatingMult()  // 1.5x to 2.1x based on party size

// One-Shot Mechanic (7+ party only)
if (partySize >= 7 && random < getBossOneShootChance()) damage = targetHp * 10
```

### Party Scaling System
Enemies scale based on party size (1-10 players):
```javascript
PARTY_SCALING.wild[size] = [HP_mult, ATK_mult, DEF_mult, SPD_mult]
// Example: 6 players = [2.0, 2.4, 1.1, 1.15] for wild enemies
```

### Nature System
Each creature has a nature that modifies stats:
```javascript
NATURES = {
    hardy:   { hp: 0,   atk: 0,   def: 0,   spd: 0 },   // Balanced
    adamant: { hp: -5,  atk: +10, def: 0,   spd: -5 },  // Offensive
    bold:    { hp: +10, atk: -5,  def: +10, spd: -15 }, // Defensive
    timid:   { hp: -10, atk: -10, def: -5,  spd: +25 }, // Speedy
    godtouched: { hp: +20, atk: +15, def: +15, spd: +10 } // Divine (Runvig only)
}
```

### Evolution System
- Creatures evolve at specific level thresholds (e.g., `evAt: [12]` or `evAt: [18, 28, 40]`)
- Use `getEvo(cid, level)` to get evolution stage (0-based)
- Evolution gives +15% stats per stage
- Sprite and name change on evolution

### Boss Progression
```
Chapter 1: Defeat Tier 1 bosses (5) → Unlock Nightmare Phase 0
Chapter 2: Defeat Tier 2 bosses (3) → Unlock Nightmare Phase 1
Chapter 3: Defeat Tier 3 bosses (4) → Unlock Nightmare Phase 2
Chapter 4: Defeat Nightmare P2 → Unlock Nightmare Phase 3
Chapter 5: Defeat Nightmare P3 → Unlock Nightmare Phase 4 (APOCALYPSE)
Post-Game: Defeat APOCALYPSE → Unlock THE CREATOR
```

---

## KEY FUNCTIONS QUICK REFERENCE

### Stats & Creatures
| Function | Line | Description |
|----------|------|-------------|
| `getLv(xp)` | ~7993 | Get level from XP |
| `getEvo(cid, lv)` | ~7995 | Get evolution stage (0-based) |
| `getStats(cid, lv, nature)` | ~7997 | Get calculated stats with nature modifiers |
| `getImg(cid, lv)` | ~8024 | Get creature image URL |
| `getMove(cid, lv, type)` | ~8025 | Get best available move for level |

### Battle Functions
| Function | Line | Description |
|----------|------|-------------|
| `startBattleWith(team, enemies, bgImg)` | ~12200 | Initialize battle state |
| `buildTurnOrder()` | ~12400 | Sort combatants by SPD |
| `nextTurn()` | ~13200 | Process next turn in queue |
| `doAction(type)` | ~13600 | Execute player action (atk/def/heal/spec) |
| `enemyAction()` | ~16000 | Execute enemy AI turn |
| `endBattle(victory)` | ~16600 | Handle battle end, XP/coin distribution |

### Scaling Functions
| Function | Line | Description |
|----------|------|-------------|
| `getPartySize()` | ~6481 | Count active students with creatures |
| `scaleWildEnemy(hp, atk, def, spd)` | ~6614 | Scale wild enemy stats |
| `scaleBoss(hp, atk, def, spd)` | ~6630 | Scale boss stats |
| `adjustEnemyDamage(dmg, enemy, target)` | ~6839 | Apply damage caps/crits |

### Rendering Functions
| Function | Line | Description |
|----------|------|-------------|
| `renderMain()` | ~9400 | Render current screen |
| `renderBattle(m)` | ~13247 | Render battle UI |
| `renderArena(m)` | ~8467 | Render PvP arena |
| `renderShop(m)` | ~9600 | Render shop screen |

---

## COMMON EDIT LOCATIONS

### To modify creature stats/abilities:
- `CREATURES` object: Lines 7373-7442
- Example creature: ~7393 (`lightning_wolf`)

### To modify boss encounters:
- `BOSSES` object: Lines 7732-7766
- Boss minions: `BOSS_MINIONS` at line ~7709
- Boss encounter start: `startBossEncounter()` ~11000

### To modify battle mechanics:
- Damage calculation: `doAction()` ~13600-14600
- Enemy AI: `enemyAction()` ~16000-16600
- Party scaling: `PARTY_SCALING` ~6521

### To modify UI/styling:
- CSS: Lines 1-6318
- Battle render: `renderBattle()` ~13247
- Victory/Defeat overlays: ~16832-16935

### To modify shop/items:
- `SHOP_ITEMS` array: Lines 6962-7173
- `REAL_REWARDS` array: Lines 7176-7277
- Shop render: `renderShop()` ~9600

### To modify nature system:
- `NATURES` object: Lines 6701-6736
- Nature application in `getStats()`: ~8014-8021

### To modify focus/special costs:
- Constants: Lines 6688-6694
- `calculateSpecialCost()`: Lines 6784-6811

---

## SPECIAL CREATURES

### Runvig - The Creator's Mythical Creature (Line ~7402)
- Only creature with `forcedNature: "godtouched"` (+20% HP, +15% ATK/DEF, +10% SPD)
- Only creature with `isMythical: true` and `creatorCreature: true`
- Has 4 evolution stages with unique moves at each stage
- Strongest base stats in the game

---

## TIPS FOR EFFICIENT EDITING

1. **Use line numbers** - "Edit around line 13600" is better than "fix combat"
2. **One change at a time** - Make focused, targeted edits
3. **Test incrementally** - Verify each change works before moving on
4. **Check for dependencies** - Many functions call each other; understand the flow
5. **Preserve existing patterns** - Match code style, variable naming, etc.

---

## VERSION HISTORY NOTES

- **v54.7**: Fixed double-damage bug, added epic boss attack animations
- **v54.6**: Reduced boss ATK scaling, reduced special costs, added heal cooldown
- **v54.3**: Added Nature system, Arena PvP mode
- **v54.1**: Added dynamic special costs, focus rebalancing

---

## PROMPT END

**Now, what would you like me to help with?**
