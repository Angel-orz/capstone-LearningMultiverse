# MAINTAINER.md — Astral Express Tutor System · Maintainer's Guide v2.0

> This file helps maintainers understand and maintain the entire system. If you need to modify any file, please read this first.
> **v2.0 Update**: Added multi-course support, teaching mode selection, review module, March character rewrite.

---

## System Architecture Overview

```
Learner ←→ Claude Code (Runtime AI)
              │
              ├── copilot-instructions.md (Entry point — auto-read by AI on startup)
              │     Added: Step Zero course selection, pre-lesson review module, post-lesson summary
              │
              ├── teacher/config/system_core.md (Core engine — always loaded)
              │     ├── §0 Teaching mode flexibility + multi-course references
              │     ├── §1 Socratic teaching method (ML-adapted version)
              │     ├── §2 Narrative rules
              │     ├── §3 Character voice quick reference (March ✨ rewritten as HSR lively style)
              │     ├── Complete lesson flow (P0-P5 + mode awareness + pre-lesson review + post-lesson update + post-lesson summary)
              │     ├── Review module (pre-lesson review + post-lesson summary)
              │     ├── Exercise system / rotation
              │     └── Drift prevention mechanism
              │
              ├── teacher/config/system_reference.md (Reference engine — loaded on demand)
              │
              ├── teacher/config/course_catalog.md        ← 📚 Added — Course catalog (multi-course entry point)
              ├── teacher/config/course_mode.md           ← 🎯 Added — Teaching mode + time estimation
              │
              └── teacher/config/knowledge_points/        ← Knowledge point coverage (split by lesson)
```

## File Responsibility Quick Reference (v2.0 Updated Version)

| File | Responsibility | Load Timing | Modification Frequency |
|------|------|---------|---------|
| `copilot-instructions.md` | Startup sequence + course selection + review module | Auto-loaded on new session | When adding courses or adjusting workflows |
| `system_core.md` | Teaching method + narrative + workflow + review module | Always | When adjusting teaching rules |
| `system_reference.md` | Full version of reference rules | Calibration/specific scenarios | When adding details |
| **`course_catalog.md`** | **📚 Course catalog** | **New session/course switching** | **When adding new courses** |
| **`course_mode.md`** | **🎯 Teaching mode definitions + time estimation** | **First selection or query** | **When adjusting mode parameters** |
| `prologue.md` | Prologue (writing benchmark) | First startup only | Rarely modified |
| `story.md` | Worldbuilding | Always | When expanding worldbuilding |
| `story_progression/*.md` | Story nodes | Loaded per lesson | When adjusting story direction |
| `characters/march.md` | March character **✨ HSR-style rewrite** | When March teaches | Append during character development |
| `characters/danheng.md` | Dan Heng character | When Dan Heng teaches | Append during character development |
| `curriculum.md` | Course outline | When querying across chapters | When textbooks are updated |
| `knowledge_points/*.md` | Knowledge point checklists (including course ID) | Loaded per lesson | Post-lesson marking |
| `learner_profile.md` | Learner profile **Added: course ID + mode preference** | Always | During course selection/mode selection |
| `runtime/progress.md` | Progress tracking **Added: course info + mode fields** | Always | Updated every lesson |
| `runtime/session_log.md` | Class log (including post-lesson summary records) | Post-lesson update | Appended every lesson |
| `runtime/review_queue.md` | Review queue **Added: course ID field** | Pre-lesson review module | May be appended every lesson |
| `runtime/mistake_log.md` | Mistake tracker | During exercises | Record mistakes immediately |
| `runtime/wechat_group.md` | Group chat records | Check on startup | Appended after lessons |
| `runtime/wechat_unread.md` | Unread group chat messages | Generated/displayed after lessons | Generated every lesson |
| `runtime/diary.md` | Learning diary | Evening lessons | Generated daily |
| `runtime/temp_math.md` | Formula drafts | When writing formulas | During teaching |
| `MAINTAINER.md` | **This file (v2.0 updated)** | During maintenance | When system is updated |
| `courses/{course_id}/runtime/` | **📦 Course-specific runtime (progress/session_log/diary)** | Post-lesson update each lesson | After each lesson |
| `courses/{course_id}/memory/` | **📦 Course-specific memory archives** | Post-lesson/review | Appended after each lesson |
| `courses/{course_id}/story_progression/` | **📦 Course-specific story nodes** | Loaded per lesson | When designing each lesson |
| `courses/{course_id}/config/knowledge_points/` | **📦 Course-specific knowledge point coverage** | Loaded per lesson/post-lesson update | Marked every lesson |

---

## v2.0 Change Log (2026-06-18)

### 1. ✨ March Character Rewrite
- **Files**: `teacher/characters/march.md`, `teacher/story.md`, `teacher/config/system_core.md §3`
- **Change**: Based on March 7th's personality traits from *Honkai: Star Rail*, fully upgraded to lively, enthusiastic, talkative, curious "sunshine of the train"
- **Preserved Elements**: Subplot background, core conflict, teaching style, relationship with Dan Heng
- **Reinforced Elements**: Faster speech, more exclamation marks, self-interruptions, explosive analogies, more expressive recognition of students

### 2. 📚 Multi-Course Support
- **New File**: `teacher/config/course_catalog.md`
- **Modified File**: `copilot-instructions.md` (added Step Zero — course selection workflow)
- **Modified File**: `teacher/config/learner_profile.md` (added `course_id` field)
- **Design Principle**: Adding subsequent courses only requires registration in `course_catalog.md` and creation of corresponding knowledge points and story nodes
- **Extension Path**: New course knowledge point files can be placed in `knowledge_points/{course_id}/` directory

### 3. 🎯 Teaching Mode (Rough/Fine) + Time Estimation
- **New File**: `teacher/config/course_mode.md`
- **Modified File**: `teacher/config/system_core.md` (pre-lesson preparation, post-lesson update, and P0 design are all affected by mode)
- **Time Estimation**: Rough mode ≈ 3 min/page, Fine mode ≈ 5-7 min/page
- **Selection Timing**: Selected at course start, mode stays consistent within the same course

### 4. 🔄 Review Module (Pre-Lesson Review + Post-Lesson Summary)
- **Added**: Systematized review module, including spaced review, pre-lesson activation, post-lesson consolidation
- **Modified File**: `teacher/config/system_core.md` (added complete "Review Module" section)
- **Modified File**: `teacher/runtime/review_queue.md` (added course ID field)
- **Modified File**: `copilot-instructions.md` (Step Two — pre-lesson review module)

---

## v2.1 Course Isolation Fix (2026-06-20)

### Background

The runtime files and story nodes for ml-yearning and kaggle-agent courses were mixed in the shared directories `teacher/runtime/` and `teacher/story_progression/`, making it easy to overwrite old course data when adding new courses. Additionally, diary.md was never generated due to the "evening only" condition.

### Fix Contents

1. **Created `teacher/courses/` course isolation directory**
   - Each course has its own `memory/`, `runtime/`, `story_progression/`, `config/knowledge_points/`
   - Old course data has been migrated to their respective directories (shared files remain untouched for compatibility)
   
2. **Diary Fix**
   - Removed "evening only" restriction → changed to generate after every lesson
   - All logs use real dates (`YYYY-MM-DD`), `Day —` placeholders are prohibited

3. **New Course Workflow**
   - Step Zero C: New course automatically creates course isolation directories
   - All post-lesson update steps point to `courses/{course_id}/` paths

### New Files

| File | Description |
|------|------|
| `teacher/courses/ml-yearning/` | ML Yearning course-specific directory |
| `teacher/courses/kaggle-agent/` | Kaggle Agent course-specific directory |
| `teacher/memory/README.md` | Memory archive index + new course creation guide |

### Modified Files

- `teacher/runtime/diary.md` — Diary generation condition (evening only → after every lesson)
- `teacher/runtime/progress.md` — Added date recording rules
- `teacher/config/system_core.md` — Post-lesson update steps 9-10
- `copilot-instructions.md` — Step Zero C new course initialization, step three path rules, post-lesson update paths, file tree

---

## Key Design Decisions

### Why 2 teachers instead of 1 or 3?
- 1 teacher: Insufficient teaching diversity, intensive week-long study becomes monotonous
- 3 teachers: Rotation complexity is too high; a short 14-lesson cycle doesn't need 3 people
- 2 teachers: March (warm/analogy/curious/energetic) and Dan Heng (cool/structure/precise) naturally complement each other, alternating keeps things fresh

### Why is the subplot climax placed at Ch.11-12 instead of earlier?
- Early stage (Ch.1-4): Needs to build teaching trust — subplot too early would overshadow teaching
- Middle stage (Ch.5-8): Best window for fragments to seep through — casual, incomplete
- Late stage (Ch.9-12): Trust has been built, subplot climax won't overwhelm teaching
- Ch.13-14: Reserved for conclusion — the climax needs an afterglow

### Why use Machine Learning Yearning as the textbook?
- 58 short chapters perfectly suit a 14-lesson split
- Emphasizes strategy and diagnosis over formula derivation — ideal for Socratic questioning
- The textbook's "diagnosis → decision" framework naturally matches Dan Heng's engineering mindset

### Why add teaching modes (rough/fine)?
- User feedback: Current teaching content was too simplified, deleted too much course material
- Fine mode covers more textbook content, preserving the user's choice
- Time estimation helps users plan their learning cycles

### Why add a pre-lesson review module?
- Spaced memory curves need active recall to maximize retention
- Review is executed before new lessons begin, not interrupting teaching rhythm
- Quick questions are enough to activate memory, no need to re-teach

---

## Common Maintenance Operations

### Adding a New Course

1. Add a new row to the course list in `course_catalog.md`, with chapter information
2. Create a new directory `{course_id}/` under `knowledge_points/`, with knowledge point files for each lesson
3. Create a new directory `{course_id}/` under `story_progression/`, with story nodes for each lesson
4. Update the default course info in `learner_profile.md` (or let the user choose on first startup)

### Adjusting Course Mode Parameters

1. Edit `teacher/config/course_mode.md`:
   - Modify the "minutes per page" parameters (rough/fine)
   - Modify the corresponding estimated times in the quick reference table
   - Adjust detailed rules for P0-P5 mode differences

### Modifying Course Progress
1. Update the course overview table in `curriculum.md`
2. Update the rotation table in `story_progression/overview.md`
3. Update the textbook page ranges in the corresponding `knowledge_points/ch{XX}.md`

### Adjusting Character Subplots
1. Modify the "past information fragments" and "subplot seed material" in the character files
2. Update the recovery plan in `story_progression/appendix.md`
3. Check whether the subplot density of affected chapters still conforms to the density matrix

### Adding New Teaching Rules
1. Determine frequency: Every round → `system_core.md`; specific scenarios → `system_reference.md`
2. If adding to system_core.md exceeds 22KB, move low-frequency rules to system_reference.md
3. Update the "Reference Rule Loading Guide" at the end of `system_core.md`

### Cold Start Test (v2.0 Update)
In a new session:
1. Send the project folder path to Claude Code
2. Observe whether the AI executes according to copilot-instructions.md's loading order:
   - Step Zero: Check course_id → none → display course catalog → select → record
   - Step Zero: Check mode_preference → none → display mode selection → select → record
   - Step One: Load core files
   - Step Two: Pre-lesson review module (check review_queue)
   - Step Three: Load current lesson content
3. First startup: detect wechat_group.md is empty → play prologue
4. Post-lesson check: whether the post-lesson summary module was executed

### Context Budget Monitoring (v2.0)

Newly added files:
- `course_catalog.md` ≈ 2KB (loaded only on first time)
- `course_mode.md` ≈ 3KB (loaded only during selection)

Does not affect the core startup budget. Core load budget maintained at ~53KB (target ≤ 55KB ✅).

```
Core load (always):
  system_core.md (~24KB) + story.md (~7KB)
  + overview.md (~3KB) + learner_profile.md (~2KB)
  + progress.md (~1KB) = ~37KB

Pre-lesson load (current lesson):
  + Character file (~12KB) + story_progression (~3KB)
  + knowledge_points (~1KB) + review_queue (~1KB)
  + wechat_group (~2KB) = ~19KB

Total pre-lesson ≈ 56KB (including new mode info, close to 55KB target ✅)
```

---

## 🚧 Known Improvement Items

- [ ] system_core.md slightly exceeds the 22KB hard limit (~24KB). Consider moving teaching demonstrations to system_reference.md in the future
- [ ] The "relationship with learner" section in character files is initially empty — needs to be appended by the AI during teaching
- [ ] No accompanying exercise book — all practice is done through Socratic questioning and in-class exercises
- [ ] The thermometer (group chat temperature changes) relies on the AI's judgment of emotional stages — automated detection could be added later
- [ ] **Added**: Multi-course support currently only has `ml-yearning` configured; adding new courses requires creating supporting files
- [ ] **Added**: The review module's automatic reminder feature — currently relies on the AI checking review_queue during pre-lesson preparation; consider adding push notifications
- [ ] **Added**: Course mode_preference currently does not support mid-course switching — if a change is needed, progress must be cleared and restarted
