# Claude Code Starter Prompt for Legends of the Wild

Copy and paste this at the start of each new Claude Code session:

---

## PROMPT START - Copy below this line:

You are working on Legends of the Wild, a classroom RPG game. The codebase is a single 13,472-line HTML file with embedded CSS and JavaScript.

**CRITICAL: Follow these rules to avoid running out of context/memory:**

### 1. ALWAYS Read CLAUDE.md First
Before doing anything, read `CLAUDE.md` - it contains a complete map of the codebase with line numbers for every section.

### 2. NEVER Read the Full HTML File
The main file `Legends_of_the_Wild_v54.html` is 13,472 lines. Always read specific line ranges:
- Use: `Read lines 11604-11700` (specific range)
- Never: `Read the whole file`

### 3. Quick Reference - Key Line Numbers
| What | Line Range |
|------|------------|
| CSS Styles | 1-4600 |
| Audio System | 4675-4809 |
| Party Scaling | 4810-5030 |
| Nature System | 5037-5108 |
| Shop/Items (RARITY) | 5252-5671 |
| Creatures Data | 5672-5699 |
| Wild Encounters | 5700-5932 |
| Bosses & Chapters | 5985-6200 |
| Render Functions | 6200-8000 |
| Arena/PvP | 8000-9000 |
| Adventure System | 9000-10000 |
| Boss Encounters | 10000-11100 |
| Battle System (doAction) | 11200-12000 |
| Battle Animations | 12000-12400 |
| Enemy AI | 12549-12900 |
| Victory/Defeat | 12900-13100 |
| Save/Load | 13400-13472 |

### 4. Work in Small Chunks
- Make ONE edit at a time
- Verify it works before moving on
- Don't try to implement multiple features in one conversation

### 5. Be Surgical with Edits
- Read only the specific function you need to modify
- Use the Edit tool with precise old_string matching
- Don't rewrite large sections unnecessarily

### 6. Skip Asset Directories
These folders contain only images - never explore them:
- Player_Creatures/, Bosses/, Minions/, Wild_Encounters/
- Backgrounds/, Environments/, Quest_Creatures/, UI_Elements/

### 7. If You Need Context
Ask me what I want instead of exploring. I can tell you:
- Which function to edit
- What the current behavior is
- What I want changed

**Now, what would you like me to help with today?**

---

## PROMPT END - Copy above this line

