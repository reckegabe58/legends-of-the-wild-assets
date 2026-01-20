# Legends of the Wild - Complete Claude Code Reference

**Version:** v54.15 | **Lines:** ~17,400 | **Last Updated:** January 2026

Copy and paste this entire document at the start of each new Claude Code session to provide full context without reading the massive HTML file.

---

## CRITICAL RULES FOR CLAUDE CODE

### 1. NEVER Read the Full HTML File
The main file `Legends_of_the_Wild_v54.html` is ~17,400 lines. **Always read specific line ranges:**
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

### CSS Sections (Lines 1-6320)
| Line Range | Section |
|------------|---------|
| 10-46 | Base Styles - Warm Amber/Sunset Theme |
| 47-232 | Creature Cards - Per-Card Element Theming |
| 233-420 | Idle Creature Animations - Element-specific |
| 380-392 | **Mini Stats CSS** - HP(red)/ATK(gold)/DEF(blue)/SPD(green)/INT(purple) |
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
| 6334-6470 | Audio System | `initAudio()`, `playSound()`, `playMusic()`, `stopMusic()` |
| 6473-6685 | Party Scaling System | `getPartySize()`, `getPartyTier()`, `PARTY_SCALING`, `scaleWildEnemy()`, `scaleBoss()` |
| 7192-7210 | **Focus System Constants** | `STARTING_FOCUS=25`, `MAX_FOCUS=100`, `BASE_FOCUS_REGEN=5`, `INT_FOCUS_MODIFIER=0.15`, `calculateFocusRegen()` |
| 7217-7260 | **NATURES Object** | 25 natures with HP/ATK/DEF/SPD/INT modifiers |
| 7260-7276 | Nature Category Helper | `getNatureCategory()` - includes 'intelligent' category |
| 7278-7282 | Random Nature | `getRandomNature()` |
| 7284-7303 | Nature Effects Display | `formatNatureEffects()` - shows INT arrows |
| 7305-7320 | Special Cost Calculation | `calculateSpecialCost()` (dynamic based on evo/power/AOE) |
| 7320-7400 | Enemy Damage Adjustment | `adjustEnemyDamage()`, `getBuffValue()`, `getPartyShieldValue()` |
| 7400-7450 | AOE Detection | `getSpecialType()`, `ELEMENT_EMOJI` |
| 7450-7680 | Shop Items (SHOP_ITEMS) | Consumables, equipment by chapter |
| 7680-7870 | Real/Classroom Rewards | `REAL_REWARDS`, `CLASSROOM_REWARDS` |
| 7900-7970 | **CREATURES Object** | All 22 player creatures with INT stats |
| 7970-8200 | **WILD_ENCOUNTERS** | By region: forest, volcano, ice, void |
| 8200-8250 | **MINIONS / BOSS_MINIONS** | Minion definitions and boss mappings |
| 8250-8300 | **BOSSES Object** | All boss definitions by tier |
| 8300-8450 | **CHAPTERS Object** | Story chapters, regions, boss gates |
| 8450-8500 | **XP_TABLE** | Level thresholds (1-50) |
| 8500-8550 | **Game State (`state`)** | Main state object structure |
| 8660-8695 | Utility Functions | `getLv()`, `getXPProg()`, `getEvo()`, `getStats()`, `getImg()`, `getMove()` |
| 8700-8850 | Boss/Chapter Logic | `canFightBoss()`, `isTierComplete()`, `canFightNightmarePhase()`, `getCurrentChapter()` |
| 8850-9050 | Shop/Migration | `migrateShopSystem()`, `migrateToV54_1()`, `migrateToV54_3_Natures()` |
| 9050-9400 | **Arena PvP System** | `ARENA_MODES`, `renderArena()`, team selection |
| 9400-9700 | Arena Battle Functions | `startArenaBattle()`, arena combat logic |
| 9700-10500 | Render Functions | `renderMain()`, `renderNav()`, `renderParty()`, `renderShop()` |
| 10500-11300 | Adventure System | `renderAdventure()`, `startAdventure()`, `startWildEncounter()` |
| 11300-12500 | Boss Encounters | `startBossEncounter()`, `spawnBossMinions()`, events |
| 12500-13300 | Battle Setup | `startBattleWith()`, `buildTurnOrder()`, battle initialization |
| 13300-13900 | **Battle Rendering** | `nextTurn()`, `renderBattle()` |
| 13900-14900 | **doAction() & Combat** | Main combat handler, damage calculation, animations |
| 14900-15500 | Animation Effects | `fireProjectile()`, `showSlashEffect()`, `showImpactEffect()`, element effects |
| 15500-16300 | Target Selection | `selectTarget()`, `selectHealTarget()`, `executeHeal()` |
| 16300-16900 | **Enemy AI** | `enemyAction()`, `executeEnemyHeal()`, boss attack patterns |
| 16900-17200 | Victory/Defeat | `endBattle()`, `showVictoryOverlay()`, `showDefeatOverlay()` |
| 17200-17450 | Level Up/Evolution | `showNextLevelUp()`, `showEvolutionSequence()` |
| 17450-17520 | Save/Load, Init | `save()`, `load()`, `resetGame()`, DOMContentLoaded |

---

## KEY DATA STRUCTURES

### `state` - Main Game State (Line ~8500)
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
    coinBoostAdventures: 0,
    curHp: undefined,       // Persisted HP (undefined = full)
    curFocus: undefined     // Persisted Focus
}
```

### Creature Definition (CREATURES object, Line ~7900)
```javascript
CREATURES = {
    lightning_wolf: {
        name: "Lightning Wolf",
        type: "Lightning",
        evo: 2,                    // Max evolution stage (2 = 2 evolutions)
        evAt: [12],                // Levels where evolution occurs
        base: { hp: 70, atk: 30, def: 16, spd: 30, int: 14 },  // v54.15: includes INT
        grow: { hp: 13, atk: 5, def: 3, spd: 5, int: 2 },      // Stats gained per level
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
    // ... more creatures (22 total)
}
```

### Boss Definition (BOSSES object, Line ~8250)
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
        st: { hp: 200, atk: 80, def: 45, spd: 65, int: 28 },  // v54.15: includes INT
        maxHp: 200,
        curHp: 180,
        focus: 25,                 // Current focus points
        focusMax: 100,
        focusRegen: 9,             // v54.15: calculated from INT (base 5 + INT*0.15)
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
        int: 12,                   // v54.15: Enemy INT for healing/focus regen
        lv: 15,
        img: "Bosses/Tier 1/...",
        isBoss: true,
        isMinion: false,
        tier: 1,
        focusRegen: 6              // v54.15: calculated from INT
    }],
    enemy: {...},                  // Primary enemy reference
    targetingMode: false,          // Attack target selection
    healTargetingMode: false,      // Heal target selection
    itemUsedThisTurn: {}           // {memberIdx: true} - tracks item usage
}
```

---

## GAME MECHANICS

### Stats System (v54.15)
The game has **5 core stats**:
| Stat | Color | Effect |
|------|-------|--------|
| HP | Red (#f87171) | Health points |
| ATK | Gold (#fbbf24) | Attack damage |
| DEF | Blue (#60a5fa) | Damage reduction |
| SPD | Green (#4ade80) | Turn order priority |
| INT | Purple (#c084fc) | Healing power & focus regen |

### INT Stat Effects (v54.15)
```javascript
// Healing Power Bonus: +0.8% per INT point
const intBonus = 1 + (healer.st.int * 0.008);
// INT 10 = +8%, INT 25 = +20%, INT 50 = +40%

// Focus Regeneration: base 5 + (INT * 0.15) per turn
const focusRegen = Math.floor(BASE_FOCUS_REGEN + (int * INT_FOCUS_MODIFIER));
// INT 10 = 6/turn, INT 20 = 8/turn, INT 30 = 9/turn
```

### INT Values by Creature Type
| Type | Base INT | Grow INT | Role |
|------|----------|----------|------|
| Light | 22-24 | 3-4 | Best healers |
| Void | 24 | 3 | Psychic/mental |
| Nature | 18-20 | 3 | Natural wisdom |
| Shadow | 18-20 | 3 | Cunning |
| Water/Ice | 16-18 | 2-3 | Balanced |
| Lightning | 14-16 | 2 | Quick-witted |
| Fire | 12-14 | 2 | Offensive |
| Earth/Metal/Bug | 10-12 | 2 | Physical |
| Mythical (Rúnvíg) | 30 | 4 | Divine |

### Combat System
- **Turn Order**: Based on SPD stat, higher goes first
- **Actions**: ATK (free), DEF (+10 Focus), HEAL (costs Focus, cooldown), SPECIAL (costs Focus, cooldown)
- **Focus**: Starts at 25, regenerates based on INT, max 100
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

### Healing Calculation (v54.15)
```javascript
const baseHeal = healer.maxHp * moveBasePower;
const levelBonus = 1 + (healer.lv * 0.01);    // +1% per level
const intBonus = 1 + (healer.st.int * 0.008); // +0.8% per INT point
const healAmount = Math.floor(baseHeal * levelBonus * intBonus);
```

### Party Scaling System
Enemies scale based on party size (1-10 players):
```javascript
PARTY_SCALING.wild[size] = [HP_mult, ATK_mult, DEF_mult, SPD_mult]
// Example: 6 players = [2.0, 2.4, 1.1, 1.15] for wild enemies
```

### Nature System (v54.15 - includes INT)
25 natures total with stat modifiers:

**Standard Natures:**
```javascript
NATURES = {
    hardy:   { hp: 0,   atk: 0,   def: 0,   spd: 0,   int: 0 },   // Balanced
    adamant: { hp: -5,  atk: +10, def: 0,   spd: -5,  int: 0 },   // Offensive
    bold:    { hp: +10, atk: -5,  def: +10, spd: -15, int: 0 },   // Defensive
    timid:   { hp: -10, atk: -10, def: -5,  spd: +25, int: 0 },   // Speedy
    calm:    { hp: +15, atk: -10, def: +5,  spd: -10, int: +5 },  // Bulky + INT
    modest:  { hp: +5,  atk: +5,  def: -5,  spd: -5,  int: +5 },  // Mixed + INT
    // ... more standard natures
}
```

**INT-Focused Natures (v54.15):**
```javascript
wise:      { hp: -5,  atk: -10, def: 0,   spd: 0,   int: +15 }, // Pure INT
sage:      { hp: -10, atk: -10, def: +5,  spd: -5,  int: +20 }, // Max INT
clever:    { hp: 0,   atk: -5,  def: -5,  spd: +5,  int: +10 }, // INT/SPD hybrid
scholarly: { hp: +5,  atk: -15, def: +5,  spd: -10, int: +15 }, // Support tank
```

**Divine Nature:**
```javascript
godtouched: { hp: +20, atk: +15, def: +15, spd: +10, int: +15 } // Runvig only
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
| `getLv(xp)` | ~8661 | Get level from XP |
| `getEvo(cid, lv)` | ~8663 | Get evolution stage (0-based) |
| `getStats(cid, lv, nature)` | ~8667 | Get calculated stats including INT with nature modifiers |
| `getImg(cid, lv)` | ~8695 | Get creature image URL |
| `getMove(cid, lv, type)` | ~8696 | Get best available move for level |
| `calculateFocusRegen(int)` | ~7207 | Get focus regen from INT stat |

### Battle Functions
| Function | Line | Description |
|----------|------|-------------|
| `startBattleWith(team, enemies, bgImg)` | ~12500 | Initialize battle state |
| `buildTurnOrder()` | ~12700 | Sort combatants by SPD |
| `nextTurn()` | ~13500 | Process next turn in queue |
| `doAction(type)` | ~13900 | Execute player action (atk/def/heal/spec) |
| `enemyAction()` | ~16300 | Execute enemy AI turn |
| `endBattle(victory)` | ~16900 | Handle battle end, XP/coin distribution |
| `showHealTargetSelection()` | ~18493 | Handle heal targeting with INT bonus |
| `executeEnemyHeal()` | ~19163 | Enemy healing with INT bonus |

### Scaling Functions
| Function | Line | Description |
|----------|------|-------------|
| `getPartySize()` | ~6481 | Count active students with creatures |
| `scaleWildEnemy(hp, atk, def, spd)` | ~6614 | Scale wild enemy stats |
| `scaleBoss(hp, atk, def, spd)` | ~6630 | Scale boss stats |
| `adjustEnemyDamage(dmg, enemy, target)` | ~7350 | Apply damage caps/crits |

### Rendering Functions
| Function | Line | Description |
|----------|------|-------------|
| `renderMain()` | ~9700 | Render current screen |
| `renderBattle(m)` | ~13500 | Render battle UI |
| `renderArena(m)` | ~9100 | Render PvP arena |
| `renderShop(m)` | ~9900 | Render shop screen |

---

## COMMON EDIT LOCATIONS

### To modify creature stats/abilities:
- `CREATURES` object: Lines 7900-7970
- All creatures have 5 stats: HP, ATK, DEF, SPD, INT

### To modify boss encounters:
- `BOSSES` object: Lines 8250-8300
- Boss minions: `BOSS_MINIONS` at line ~8220
- Boss encounter start: `startBossEncounter()` ~11300

### To modify battle mechanics:
- Damage calculation: `doAction()` ~13900-14900
- Enemy AI: `enemyAction()` ~16300-16900
- Party scaling: `PARTY_SCALING` ~6521

### To modify UI/styling:
- CSS: Lines 1-6320
- Mini stats colors: Lines 380-392 (includes INT purple)
- Battle render: `renderBattle()` ~13500
- Victory/Defeat overlays: ~17000-17100

### To modify shop/items:
- `SHOP_ITEMS` array: Lines 7460-7680
- `REAL_REWARDS` array: Lines 7680-7870
- Shop render: `renderShop()` ~9900

### To modify nature system:
- `NATURES` object: Lines 7217-7258
- INT-focused natures: wise, sage, clever, scholarly (lines 7250-7255)
- Nature application in `getStats()`: ~8683-8691

### To modify INT/focus/healing system:
- Focus constants: Lines 7192-7210
- `calculateFocusRegen()`: Line ~7207
- Healing formula: `showHealTargetSelection()` ~18497-18505
- Enemy healing: `executeEnemyHeal()` ~19163-19167

---

## SPECIAL CREATURES

### Runvig - The Creator's Mythical Creature (Line ~7930)
- Only creature with `forcedNature: "godtouched"` (+20% HP, +15% ATK/DEF, +10% SPD, +15% INT)
- Only creature with `isMythical: true` and `creatorCreature: true`
- Has 4 evolution stages with unique moves at each stage
- Base INT: 30, Grow INT: 4 (highest in game)
- Strongest base stats in the game

---

## TIPS FOR EFFICIENT EDITING

1. **Use line numbers** - "Edit around line 13900" is better than "fix combat"
2. **One change at a time** - Make focused, targeted edits
3. **Test incrementally** - Verify each change works before moving on
4. **Check for dependencies** - Many functions call each other; understand the flow
5. **Preserve existing patterns** - Match code style, variable naming, etc.

---

## VERSION HISTORY NOTES

- **v54.15**: Added INT stat - affects healing (+0.8%/point) and focus regen (base 5 + INT*0.15). Added 4 INT natures (wise, sage, clever, scholarly). UI displays INT with 🧠 in purple.
- **v54.14**: Major update - Boss AI, Elite Enemies, Ally Quests, Individual Healing
- **v54.13**: Epic special animations, custom arena battles, wild attack animations
- **v54.8**: Fixed fireProjectile element size error, fixed double-damage bug with action ID tracking
- **v54.7**: Fixed double-damage bug, added epic boss attack animations
- **v54.6**: Reduced boss ATK scaling, reduced special costs, added heal cooldown
- **v54.3**: Added Nature system, Arena PvP mode
- **v54.1**: Added dynamic special costs, focus rebalancing

---

## PROMPT END

**Now, what would you like me to help with?**
